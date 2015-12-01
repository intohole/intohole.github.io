---
layout: post  
tags: [ml,translate]   
title: dive into machine learning翻译    
city: 北京 
---

HI , 看这里， 这是一个给你的指引
==================
+ 刚了解机器学习
+ 你会使用python.(至少是一个基础！你如果想学习python，可以试着[Dive into Python](http://www.diveintopython.net/)


为了第一次hacking，我学习了python，之后又去不断深入；我用它做机器学习，如果你也深谙此道，跟我一起变的强大；

### 注意:这里有几个关于"数据"的名词，而机器学习只是其中之一，了解这些名词，会对你理解本文有很大帮助:数据分析、数据挖掘、数据科学、机器学习和大数据有什么区别呢？ ###


让我们去尝试去做吧！
--------
我的建议是：去自己使用下，这样会提高你的自信


你需要的工具列表
-------
+ python . Python 3 是最好的选择。
+ IPython和jupyter学习日记
+ 一些科学计算包
	+ numpy
	+ pandas
	+ scikit-learn
	+ matplotlib

你可以安装Python3和以上所有包裹，只需要在[Anaconda Python distribution](https://www.continuum.io/downloads).Anaconda是非常受欢迎的数据科学和机器学习论坛；   
如果你使用python2.7，也不要担心；你可以不用迁移到Python3;另外，如果你使用pip/virtualenv去替代Anaconda，这样也是可以哦！可以参照[ conda vs. pip vs. virtualenv](http://conda.pydata.org/docs/_downloads/conda-pip-virtualenv-translator.html)  
  

让我们开始吧！
--------------
[学习怎么使用IPython笔记](http://opentechschool.github.io/python-data-intro/core/notebook.html)(5-10分钟).  
现在，跟着[一个介绍机器学习模型scikit-learn文档](http://scikit-learn.org/stable/tutorial/basic/tutorial.html)(10分钟)。并且使用ipython或者ipython笔记。它真的会提高你的自信。  
![图1-1](http://i.imgur.com/nqn3pVV.jpg)
刚刚发生了什么？
-------
你刚刚用[sciki-learn](http://hangtwenty.github.io/dive-into-machine-learning/),对手写数字进行了区分，很爽吧？  
[sciki-learn](http://hangtwenty.github.io/dive-into-machine-learning/)是一个python版本机器学习类库。机器学习是困难的，你会非常高兴你有这样的工具，可以简单的去解决它；  
  我非常鼓励你花5分钟，或者更多的时间，去浏览[sciki-learn](http://hangtwenty.github.io/dive-into-machine-learning/)主页，去了解一些名称（分类、回归等），以及他们的使用场景。不要去点击进入里面去看详细内容，你只需要过目就可以了。  

深入部分
---------
### 图解机器学习 ###
让我们对机器学习了解再多一点，一些通用的想法和理念。阅读[图解机器学习](http://www.r2d3.us/visual-intro-to-machine-learning-part-1/)，这篇文章的作者[Stephanie Yee](https://twitter.com/stephaniejyee)和[Tony chu](https://twitter.com/tonyhschu/)   
![图解2](http://i.imgur.com/j5fiTBv.gif)
它不会花费你很长时间的！它介绍的很漂亮，到时要控制住自己的口水哦！
好的。让我们更加理解更深点！  
来让我阅读Pedro Domingos写的[几个非常有用机器学习建议](http://homes.cs.washington.edu/~pedrod/papers/cacm12.pdf)，写的很有干货而且还简单明了。作者了解很多窍门，而且展示给你。   
花些时间去了解它，最好记下笔记。不要担心你现在不是很了解。  
整篇论文写了很多要点。但是我要指出其中我认为重要的两点：     

+ 不仅仅只是数据：机器学习是一门科学艺术。引用Domingos的话来说:"所需要了解的知识不会那么晦涩。机器学习不是魔术；它不会无中生有，只是从很少的信息，来获取更多你所需要的信息。编程：像大多数的工程，它大多数的工作：我们不得不从很多条框上建立；机器学习更像耕种，让自然环境做大多数的工作，农民播种通过吸收营养来使得其成长。机器学习者更像组合知识来让数据获得方程式；”

+ 更多的数据，比一个聪明的算法更加重要：仔细听，程序猿们！我们喜欢酷的工具，抵制重复建造轮子的诱惑，不要过工程师；你应该专注的是，做最简单的事情，来尽可能使其工作。引用Domingos的话来说：“你已经尽最大可能建立最好的属性，但是分类器还没有达到你的要求。这时候你能做什么？这里有两个选择：设计更好的算法或者获得更多的数据。一个有充足数据稍微差的分类器会打败一个有少量数据的聪明算法”

所以### 知识 ###和### 数据 ###都是非常重要的。集中精力在这些方面上，而非只看重算法本身。在实践中，这就意味着你万不得已时才增加复杂性，否则你应该做简单的事情；不要一上来就用神经网络，只是因为它足够酷炫。提高你模型，通过得到更多的数据和对问题理解的来使用数据。应该花费你的时间在这些方面上。优化算法应该在你得到足够的数据，并且你处理的很好之后的事情。
![图解3](http://i1381.photobucket.com/albums/ah240/hangtwenty/Screen%20Shot%202015-03-05%20at%2010.08.10%20PM_zpsqnljkqt5.png)

Talk machines
-------------
订阅[Talk Machines](http://www.thetalkingmachines.com/),这是一个关于机器学习的博客，它很高效让你收获知识。  
我建议的听的顺序:  
+ 从“[Strart simple](http://www.thetalkingmachines.com/blog/2015/4/23/starting-simple-and-machine-learning-in-meds)”章节开始。它看起来像是Domingos所写.Admas建议从简单开始，就像我上面所赘述的一样。Admas会集中大量精力，在属性建设方面。属性建设就是知识的升华。
+ 然后，从第一章节开始。

从玩中学习
------------
从IPython笔记中挑选一到两个,玩耍一下！   
+ 在一堆标记号脸上做人脸识别
+ 从灾难中机器学习：使用Titanic数据，分析和可视化技术，用演示基本模型。展示一些监督学习例子。
+ 预测选举：复制Nate Silver为纽约时代杂志对2012年美国总统选举的预测。
+ 一个机器学习笔记的例子:"我们正在为一家创业公司工作，这家公司想用手机自动识别拍照花卉类别,我们根据对数据的理解，创建一个拥有四个关于花度量（花萼长度，花萼的宽度，花瓣的长度，花瓣的宽度）的机器学习demo，通过这四维属性，识别花的种类"
+ 点击安全的"数据hacking"系列（感谢[hummus!](https://github.com/hummus)）
	+ 检测自动生成主域
	+ 检测sql注入
	+ Java class 文件分析：判断是恶意代码还是友好代码？
+ 如果你想获得更多数据科学，可以翻阅下[杰出的数据科学ipython笔记](https://github.com/donnemartin/data-science-ipython-notebooks)。（持续更新数据可续Python笔记:Spark,Hadoop MapReduce,HDFS,AWS,Kaggle,scikit-learn,matplotlib,pandas,NumPy,Scipy,Various命令行）
+ 或者更多的通用教程/概述。。。
	- [sklearn机器学习教程](http://amueller.github.io/sklearn_tutorial/)
	- [通过scikit learn监督学习教程](http://bugra.github.io/work/notes/2014-11-22/an-introduction-to-supervised-learning-scikit-learn/)
	- [通过scikit learn无监督机器学习介绍](http://bugra.github.io/work/notes/2014-11-16/an-introduction-to-unsupervised-learning-scikit-learn/)

还有更多的地方可以找到非常好的Ipython笔记
+ [一个非常有趣的IPython笔记图库(wiki 页保存在 GitHub上):统计学，机器学习和数据科学。](https://github.com/ipython/ipython/wiki/A-gallery-of-interesting-IPython-Notebooks#statistics-machine-learning-and-data-science)
+ [费边Pedregosa更大，自动图解](http://nb.bianp.net/sort/views/)

让自己深入专研
----------
+ 选择下面的一个课程，并且完成它。

推荐课程
------------
[ 教授Andrew Ng的机器学习在线课程 ](https://www.coursera.org/learn/machine-learning) 这是一个免费的在线教程，我经常推荐,并且是一个重点 。    
创建一个玩具工程，去运用你学习到的知识，是很有帮助的。你可以使用一个[杰出的数据集](https://github.com/caesar0301/awesome-public-datasets).还有记住，Ipython笔记是你学习的伴侣。

还有，[Elements of Statistical Learning(统计学习元素)](http://statweb.stanford.edu/~tibs/ElemStatLearn/)经常出现，但是它通常作为一个参考的援引，而不是作为一个介绍。它是免费的，可以下载下来或者弄成标签页。

其它课程
--------
下面是我推荐一些其它在线教程。（机器学习，数据科学和其它相关的主题）
+ [机器学习](https://www.coursera.org/course/machlearning)由 华盛顿大学的Pedro Domingos教授; 前面介绍了Domingos教授论文“[A Few Useful Things to Know About Machine Learning](https://homes.cs.washington.edu/~pedrod/papers/cacm12.pdf)”(谢谢Hacker News 论文工作)




参考
------------------
+ [Dive into machine learning](http://hangtwenty.github.io/dive-into-machine-learning/)
+ [scikit-learn一些经验](http://scikit-learn.org/stable/tutorial/machine_learning_map/)