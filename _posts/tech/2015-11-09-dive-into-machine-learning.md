---
layout: post  
tags: [tech,ml]   
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






参考
------------------
+ [Dive into machine learning](http://hangtwenty.github.io/dive-into-machine-learning/)
+ [scikit-learn一些经验](http://scikit-learn.org/stable/tutorial/machine_learning_map/)