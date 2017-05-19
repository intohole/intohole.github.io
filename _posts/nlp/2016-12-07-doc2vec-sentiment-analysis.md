---
layout: post  
tags: [nlp]   
title:	基于Doc2Vec情感分析（翻译）
city: 杭州
---

使用Doc2Vec情感分析
======================
Word2Vec是神奇的东西。总之，它能从一个文档集中，将文档中的词转换为向量。你会问这些向量有什么特别吗？是的，一些语义相近的词会离彼此近一些。更多的是，这些向量表示，我们如何使用这些单词。例如，v_man - v_woman约等于v_king - v_queen，说明“男人相对于女人类似皇帝对应女王”。这个过程中，自然语言处理魔术，被称为词编码。这种替代方法得到了广泛应用。Doc2Vec不是指代词，而是一个句子或者一篇文章，这正是它杰出的方面。想象一下，用固定长度向量代表整个句子，并能运行所有标准的分类算法。这样做是不是很神奇呢？

然而，Word2Vec文档不友好。C 代码阅读起来费力（700行代码是高度优化的，有很多编码技巧）。我个人花了大量的时间解决Doc2Vec由于错误引起大约50%精度错误。本教程的目的是帮助其他用户使用Word2Vec在自己的研究上取得进展。我们在康奈尔大学的IMDB电影评论文集，使用Word2Vec进行情感分析。（http://www.cs.cornell.edu/people/pabo/movie-review-data/）进行分类。

在这个演示中使用的源代码可以在[https://github.com/linanqiu/word2vec-sentiments](https://github.com/linanqiu/word2vec-sentiments)找到

建立
---------

模块
------------

我们使用gensim，因为gensim有一个更可读的Word2Vec（Doc2Vec）的实现。幸亏那些家伙。我们还使用了numpy数组操作和用sklearn逻辑回归作为分类器。       

```
    # gensim modules
    from gensim import utils
    from gensim.models.doc2vec import LabeledSentence
    from gensim.models import Doc2Vec

    # numpy
    import numpy

    # random
    from random import shuffle

    # classifier
    from sklearn.linear_model import LogisticRegression
```

输入格式
------------
我们不能直接使用康奈尔大学的电影原始数据评论。相反，我们要将他们转换为小写字母，并移除标点符号。我是通过bash完成这件事情的，你也可以通过Python，JS，或者你喜欢的脚本语言，做到这一点很容易。这一步是微不足道的。

其结果是有5个文件：       

+ test-neg.txt：从试验数据12500消极电影评论   
+ test-pos.txt：从试验数据12500积极电影评论
+ train-neg.txt：从训练数据12500积极电影评论
+ train-pos.txt：从训练数据12500消极电影评论
+ train-unsup.txt：50000未标记的电影评论

每个的审查每个格式应为这样的：

```
once again mr costner has dragged out a movie for far longer than necessary aside from the terrific sea rescue sequences of which there are very few i just did not care about any of the characters most of us have ghosts in the closet and costner s character are realized early on and then forgotten until much later by which time i did not care the character we should really care about is a very cocky overconfident ashton kutcher the problem is he comes off as kid who thinks he s better than anyone else around him and shows no signs of a cluttered closet his only obstacle appears to be winning over costner finally when we are well past the half way point of this stinker costner tells us all about kutcher s ghosts we are told why kutcher is driven to be the best with no prior inkling or foreshadowing no magic here it was all i could do to keep from turning it off an hour in
this is an example of why the majority of action films are the same generic and boring there s really nothing worth watching here a complete waste of the then barely tapped talents of ice t and ice cube who ve each proven many times over that they are capable of acting and acting well don t bother with this one go see new jack city ricochet or watch new york undercover for ice t or boyz n the hood higher learning or friday for ice cube and see the real deal ice t s horribly cliched dialogue alone makes this film grate at the teeth and i m still wondering what the heck bill paxton was doing in this film and why the heck does he always play the exact same character from aliens onward every film i ve seen with bill paxton has him playing the exact same irritating character and at least in aliens his character died which made it somewhat gratifying overall this is second rate action trash there are countless better films to see and if you really want to see this one watch judgement night which is practically a carbon copy but has better acting and a better script the only thing that made this at all worth watching was a decent hand on the camera the cinematography was almost refreshing which comes close to making up for the horrible film itself but not quite
```

上面包含了两种极性(积极/消极)电影评论,每个都独立占据一行，是的，每个文档都要在一行，并且用换行符分割。这是非常重要的，因为我们通过换行符解析出每个句子(文档)；

数据塞入到Doc2Vec
---------------------
Doc2Vec（gensim实现Doc2Vec算法）在词编码上做了一个伟大的工作，但是当它遇到多文件的时候，是比较头疼的事情。它的LabeledLineSentence原生类，只返回LabeledSentence,这是gensim.models.doc2vec用来代表一个单句的。为什么“标记”词？这个就是Doc2Vec和Word2Vec的不同之处。

Word2Vec只是一个词转换成向量。

Doc2Vec不仅仅这样做，而且还要将一个句子转换为一个向量。要做到这一点，把句子到标记作为一个特殊的词，并且在这个特殊的词中采用一些特殊手段。因此，这些特殊的词是一个句子的标记。

因此，我们必须将句子转化成

```
[['word1', 'word2', 'word3', 'lastword'], ['label1']]
```
LabeledSentence就是干净利落的实现这个方法。它包含的单词列表，并为句子的标签。我们并不真正需要关心的是如何LabeledSentence工作的准确，我们只需要知道，它存储这两件事情-单词和标签的列表。

但是，我们需要一种方法来我们的新行分隔语料转化成的集合LabeledSentence秒。默认的默认构造函数LabeledLineSentence中Doc2Vec类可以做到这一点对一个文本文件，但不能这样做，对于多个文件。在分类任务然而，我们通常处理多个文档（试验，训练，积极的，消极等）。是不是很烦？

因此，我们写我们自己的LabeledLineSentence类。构造函数中定义的文件，翻翻词典和标签前缀从该文件的句子应该承担。然后，Doc2Vec可以直接经由迭代读取的收集，或者我们可以直接访问阵列。我们还需要一个函数返回数组的一个置换的版本LabeledSentence秒。我们就会明白为什么后来。

```
class LabeledLineSentence(object):
    def __init__(self, sources):
        self.sources = sources
        
        flipped = {}
        
        # make sure that keys are unique
        for key, value in sources.items():
            if value not in flipped:
                flipped[value] = [key]
            else:
                raise Exception('Non-unique prefix encountered')
    
    def __iter__(self):
        for source, prefix in self.sources.items():
            with utils.smart_open(source) as fin:
                for item_no, line in enumerate(fin):
                    yield LabeledSentence(utils.to_unicode(line).split(), [prefix + '_%s' % item_no])
    
    def to_array(self):
        self.sentences = []
        for source, prefix in self.sources.items():
            with utils.smart_open(source) as fin:
                for item_no, line in enumerate(fin):
                    self.sentences.append(LabeledSentence(utils.to_unicode(line).split(), [prefix + '_%s' % item_no]))
        return self.sentences
    
    def sentences_perm(self):
        shuffle(self.sentences)
        return self.sentences
```



现在，我们可以将多个文件塞入到  LabeledLineSentence 。正如我们前面提到的，LabeledLineSentence接受一个简单的词典类型，键是文件名和值一个特殊的前缀，这个前缀一定要不同，这是为了标记每个句子的不同来源（训练数据集不同）

我们将前缀加上了一个计数器，这样就使每个句子都有了不同的标记。       


```
sources = {'test-neg.txt':'TEST_NEG', 'test-pos.txt':'TEST_POS', 'train-neg.txt':'TRAIN_NEG', 'train-pos.txt':'TRAIN_POS', 'train-unsup.txt':'TRAIN_UNS'}
sentences = LabeledLineSentence(sources)
```



模型
---------------
构建词汇表
---------------


Doc2Vec要求我们建立的词汇表（简单的过滤所有词，并且做了一个基础的计数）。所以，我们要塞入所有句子。model.build_vocab接受LabeledLineSentence数组，因此我们的to_array功能的LabeledLineSentences类。

如果你对参数好奇，可以阅读Word2Vec文档。其它的，这里是一个简要介绍：

+ min_count：忽略词总频率低于这个所有的单词。你必须将它设置为1，因为句子的标签只出现一次。设置任何高于1将错过句子。
+ window：一个句子内的当前和预测的字之间的最大距离。Word2Vec使用skip-gram的模型，这个对窗口的大小设置简单。
+ size：输出向量的维数。100是一个不错的数字。如果你极端的，你可以到400左右。
+ sample：阈值配置这更高频率的话是随机下采样
+ workers：设置线程数目去训练这个模型。

```
model = Doc2Vec(min_count=1, window=10, size=100, sample=1e-4, negative=5, workers=8)

model.build_vocab(sentences.to_array())
```
训练Doc2Vec
------------
现在我们训练模型。一个句子输入到模型中是序列是随机的，我们可以迭代训练。这一点很重要：如果你没有这个步骤，你可能得到一个非常糟糕的结果。这就是在LabeledLineSentences的类，sentences_perm有这个方法的原因。

我们迭代10次，如果你有更多的时间，我做过迭代20次的。

这个过程大约要进行10分钟左右，你可以喝一些咖啡。

```
for epoch in range(10):
    model.train(sentences.sentences_perm())
```
保存和重载模型
------------
为了避免再次训练模型，我们可以将它保存。


```
model.save('./imdb.d2v')
```

重载它

```
model = Doc2Vec.load('./imdb.d2v')
```



实验模型
------------------
让我们来看看我们的模型给出。它似乎已经那种理解这个词good，因为最相似的词好有glamorous，spectacular，astounding等。这实在是真棒（重要），因为我们正在做的情感分析。


```
model.most_similar('good')

[(u'excellent', 0.49283793568611145),
 (u'rudolfs', 0.43693652749061584),
 (u'chattanooga', 0.4162406325340271),
 (u'dodgy', 0.4156044125556946),
 (u'hurts', 0.4120287299156189),
 (u'maytime', 0.4106871485710144),
 (u'problematic', 0.4097048342227936),
 (u'lousy', 0.40627604722976685),
 (u'humanization', 0.40399202704429626),
 (u'detaches', 0.40335381031036377)]
```


我们可以看下模型中到底含有什么。这是模型中一个词和句子的向量。我们可以通过访问model.syn0（对你们中间那些极客，syn0是浅神经网络的输出层）。但是，我们对单个词的向量没有兴趣，我们更想要的是一个句子的向量。

这个是我们一个消极的训练样本句子向量样本：


```
model[ 'TRAIN_NEG_0' ]
array([-0.29009071, -0.12225933,  0.31921104,  0.12690307, -0.78038144,0.22722125,  0.20833154,  0.43868524,  0.23561548, -0.36413202,-0.15643257,  0.00461203,  0.08018852, -0.08258788, -0.2760058 ,0.10478264, -0.08799575, -0.37180164, -0.33013585,  0.18241297,0.88061708,  0.31900761,  0.23834513, -0.10049706,  0.28829831,-0.10783304,  0.0262799 ,  0.14395693, -0.10469725, -0.52104455,-0.65519089,  0.55344343,  0.01129826,  0.04632513, -0.15539262,
-0.28914869,  0.33816752, -0.62154663, -0.02470196,  0.62869382,0.11478873, -0.25910828, -0.08567604, -0.02737088, -0.07904764,-1.01183033, -0.17131189,  0.04178049, -0.25471294, -0.42550623,-0.58592063, -0.31924966,  0.17547569,  0.20776786, -0.34506091,0.00154094,  0.30706513,  0.09242618,  0.02120452, -0.09602273,-0.40714192,  0.47554722,  0.36416441,  0.01952979,  0.6814065 ,-0.15965664, -0.22644502, -0.24989423,  0.40612498,  0.27820811,-0.35662967,  0.27260619,  0.07444458, -0.40855888,  0.09954116,0.11635212, -0.13925125,  0.18950833,  0.10479139, -0.17033359,0.06540342, -0.01675605,  0.00690889, -0.06219884,  0.13443422,0.05676769, -0.19048406, -0.08656956,  0.16460682, -0.18292029,0.42254189,  0.23022693, -0.10003133, -0.52825296,  0.18979053,-0.10800292,  0.01646511, -0.00504603,  0.173182  ,  0.19618541], dtype=float32)
```


情感分类
--------------



训练向量
-----------



现在让我们使用这些向量来训练一个分类器。首先，我们必须提取这些训练向量。请记住，我们一共有25000条训练，具有积极和消极的数量相等（12500 积极，12500 消极）。

因此，我们创建了一个numpy数组（因为我们只用分类需要numpy的阵列有两个平行的阵列，包含向量（train_arrays）和包含标签（train_labels）。

我们简单的将积极放在数据中第一部分，消极训练样本在第二个



```
train_arrays = numpy.zeros((25000, 100))
train_labels = numpy.zeros(25000)

for i in range(12500):
    prefix_train_pos = 'TRAIN_POS_' + str(i)
    prefix_train_neg = 'TRAIN_NEG_' + str(i)
    train_arrays[i] = model[prefix_train_pos]
    train_arrays[12500 + i] = model[prefix_train_neg]
    train_labels[i] = 1
    train_labels[12500 + i] = 0
```

这个训练数组看起来是这样的，行和行是每个句子的向量

```
print train_arrays

    [[ 0.18376358  0.14441976  0.09568384 ..., -0.28158343  0.29901281
   0.30613518]
    [-0.24681839  0.71076155 -0.40998992 ...,  0.39490703 -0.0812839
   0.21507834]
    [-0.05608005  0.48018554  0.35442445 ...,  0.28135905 -0.3482835
   0.23772541]
 ..., 
    [-0.23058473  0.03048714  0.8894285  ..., -0.5808149   0.18430299
  -0.08481987]
    [ 0.33824882  0.32103017 -0.24168059 ...,-0.55988938  0.61781228-0.4085339 ]
    [ 0.3712599  -0.18826039  0.30162022 ...,-0.21118143  0.00217488-0.4914557 ]]
 ```
 

该标签只是为了一句载体类别标签 : 1代表积极／0代表消极。

```   
      print train_labels
```

[ 1.  1.  1. ...,  0.  0.  0.]


测试向量
---------------


我们同样的过程组建测试样本，用来评估我们的模型好坏。


```
test_arrays = numpy.zeros((25000, 100))
test_labels = numpy.zeros(25000)

for i in range(12500):
    prefix_test_pos = 'TEST_POS_' + str(i)
    prefix_test_neg = 'TEST_NEG_' + str(i)
    test_arrays[i] = model[prefix_test_pos]
    test_arrays[12500 + i] = model[prefix_test_neg]
    test_labels[i] = 1
    test_labels[12500 + i] = 0

```

分类
----------------

现在我们用训练数据训练logistic分类器。

```
classifier = LogisticRegression()
classifier.fit(train_arrays, train_labels)
    LogisticRegression(C=1.0, class_weight=None, dual=False, fit_intercept=True,intercept_scaling=1, penalty='l2', random_state=None, tol=0.0001)
```


我们得到了近87％的准确度在情感分析上。这是相当惊人的，因为我们只使用线性SVM和一个很浅的神经网络。          


```
classifier.score（test_arrays，test_labels）
```


0.87312000000000001

这不是梦幻？希望我可以节省你一些时间！

参考
-------------
+ [Doc2vec：https://radimrehurek.com/gensim/models/doc2vec.html](https://radimrehurek.com/gensim/models/doc2vec.html)
+ [论文：http://arxiv.org/abs/1405.4053](http://arxiv.org/abs/1405.4053)
+ [Sentiment Analysis Using Doc2Vec](http://linanqiu.github.io/2015/10/07/word2vec-sentiment/)
