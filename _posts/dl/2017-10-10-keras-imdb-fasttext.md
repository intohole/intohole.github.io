---
layout: default
tags: [dl]
city: 杭州
title: keras fasttext例子代码解析
---

```python
'''这是一个用fasttext进行文本分类的例子

基于 oulin et al 的论文:

文本分类上的词袋技巧
https://arxiv.org/abs/1607.01759
论文注释：
    首先，扩展特征，进行序号编译
    其次，通过embeding层，将每个词进行编码
    最后，通过全联接，对应每个分类标记，迭代
我们在IMDB数据集使用Uni-gram（单个词）和bi-gram(两个词)词编码:
Results on IMDB datasets with uni and bi-gram embeddings:
    Uni-gram: 在5轮迭代后，我们得到0.8813准确率 . 在i7处理器上8s/迭代 .
    Bi-gram : 0.9056 test accuracy after 5 epochs. 2s/epoch on GTx 980M gpu.
'''

from __future__ import print_function
import numpy as np

from keras.preprocessing import sequence
from keras.models import Sequential
from keras.layers import Dense
from keras.layers import Embedding
from keras.layers import GlobalAveragePooling1D
from keras.datasets import imdb


def create_ngram_set(input_list, ngram_value=2):
    """
    从整数数组中抽取n-grams去重set

    >>> create_ngram_set([1, 4, 9, 4, 1, 4], ngram_value=2)
    {(4, 9), (4, 1), (1, 4), (9, 4)}

    >>> create_ngram_set([1, 4, 9, 4, 1, 4], ngram_value=3)
    [(1, 4, 9), (4, 9, 4), (9, 4, 1), (4, 1, 4)]
    """
    return set(zip(*[input_list[i:] for i in range(ngram_value)]))


def add_ngram(sequences, token_indice, ngram_range=2):
    """
    通过n-gram，来扩充输入参数sequnences序列；

    例子：添加一元文法
    >>> sequences = [[1, 3, 4, 5], [1, 3, 7, 9, 2]]
    >>> token_indice = {(1, 3): 1337, (9, 2): 42, (4, 5): 2017}
    >>> add_ngram(sequences, token_indice, ngram_range=2)
    [[1, 3, 4, 5, 1337, 2017], [1, 3, 7, 9, 2, 1337, 42]]

    例子：添加二元文法
    >>> sequences = [[1, 3, 4, 5], [1, 3, 7, 9, 2]]
    >>> token_indice = {(1, 3): 1337, (9, 2): 42, (4, 5): 2017, (7, 9, 2): 2018}
    >>> add_ngram(sequences, token_indice, ngram_range=3)
    [[1, 3, 4, 5, 1337], [1, 3, 7, 9, 2, 1337, 2018]]
    """
    new_sequences = []
    for input_list in sequences:
        new_list = input_list[:]
        for i in range(len(new_list) - ngram_range + 1):
            for ngram_value in range(2, ngram_range + 1):
                ngram = tuple(new_list[i:i + ngram_value])
                if ngram in token_indice:
                    new_list.append(token_indice[ngram])
        new_sequences.append(new_list)

    return new_sequences

# 设置参数:
# ngram_range = 2 会添加 bi-gram（二元文法） 文本特征 
ngram_range = 1
max_features = 20000
maxlen = 400
batch_size = 32
embedding_dims = 50
epochs = 5

print('Loading data...')
(x_train, y_train), (x_test, y_test) = imdb.load_data(num_words=max_features)
print(len(x_train), 'train sequences')
print(len(x_test), 'test sequences')
print('Average train sequence length: {}'.format(np.mean(list(map(len, x_train)), dtype=int)))
print('Average test sequence length: {}'.format(np.mean(list(map(len, x_test)), dtype=int)))

if ngram_range > 1:
    print('Adding {}-gram features'.format(ngram_range))
    #  从训练数据集中，创建n-gram去重set
    ngram_set = set()
    for input_list in x_train:
        for i in range(2, ngram_range + 1):
            set_of_ngram = create_ngram_set(input_list, ngram_value=i)
            ngram_set.update(set_of_ngram)
    # 对n-gram词产出不同序号的词典
    # 这些序号的值要大于max_features 
    # Integer values are greater than max_features in order
    # 去避免跟已有的特征重合
    start_index = max_features + 1
    # 词 -> 序号
    token_indice = {v: k + start_index for k, v in enumerate(ngram_set)}
    # 序号 -> 词
    indice_token = {token_indice[k]: k for k in token_indice}

    # max_features is the highest integer that could be found in the dataset.
    # 需要更新max_features
    max_features = np.max(list(indice_token.keys())) + 1

    # 对x_train和x_test用n-grams特征进行扩充
    x_train = add_ngram(x_train, token_indice, ngram_range)
    x_test = add_ngram(x_test, token_indice, ngram_range)
    print('Average train sequence length: {}'.format(np.mean(list(map(len, x_train)), dtype=int)))
    print('Average test sequence length: {}'.format(np.mean(list(map(len, x_test)), dtype=int)))

print('Pad sequences (samples x time)')
# 截断补齐
x_train = sequence.pad_sequences(x_train, maxlen=maxlen)
x_test = sequence.pad_sequences(x_test, maxlen=maxlen)
print('x_train shape:', x_train.shape)
print('x_test shape:', x_test.shape)

print('Build model...')
model = Sequential()

# we start off with an efficient embedding layer which maps
# our vocab indices into embedding_dims dimensions
# 
# 进行编码
model.add(Embedding(max_features,
                    embedding_dims,
                    input_length=maxlen))

# 添加 GlobalAveragePooling1D,用来将整个文档所有词embedding进行归一化
# {w1,w2 -> doc1} ; w1.vector = [1,2] ; w2.vector = [2,1] ; doc1 -> [1.5,1.5]
model.add(GlobalAveragePooling1D())

# 增加一个全联接，作为输出层，激活函数为sigmoid , 输出层是一个多个分类
model.add(Dense(1, activation='sigmoid'))

model.compile(loss='binary_crossentropy',
              optimizer='adam',
              metrics=['accuracy'])

model.fit(x_train, y_train,
          batch_size=batch_size,
          epochs=epochs,
          validation_data=(x_test, y_test))
```
参考文章
----

+ [keras lstm例子](https://github.com/fchollet/keras/blob/master/examples/imdb_fasttext.py)
