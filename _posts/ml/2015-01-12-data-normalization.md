---
layout: post
title: 归一化
tags: [ml]
---
归一化
=========
数据标准化（归一化）处理是数据挖掘的一项基础工作，不同评价指标往往具有不同的量纲和量纲单位，这样的情况会影响到数据分析的结果，为了消除指标之间的量纲影响，需要进行数据标准化处理，以解决数据指标之间的可比性。原始数据经过数据标准化处理后，各指标处于同一数量级，适合进行综合对比评价。以下是两种常用的归一化方法：

+ min-max标准化（Min-Max Normalization）
也称为离差标准化，是对原始数据的线性变换，使结果值映射到[0 - 1]之间。转换函数如下：  

<p align="center"><img src="http://latex.codecogs.com/gif.latex?\\x^{*}=(x-min)/(max - min)" title="min-max标准化" /></p>

+ Z-score标准化方法
这种方法给予原始数据的均值（mean）和标准差（standard deviation）进行数据的标准化。经过处理的数据符合标准正态分布，即均值为0，标准差为1，转化函数为：  

<p align="center"><img src="http://latex.codecogs.com/gif.latex?\\x^{*}=(x-\mu)/\varphi" title="z-score标准化" /></p>

 其中<img src="http://latex.codecogs.com/gif.latex?\mu" title="均值"/>为所有样本数据的均值，<img src="http://latex.codecogs.com/gif.latex?\varphi" title="标准差"/>为所有样本数据的标准差。

+ 对数函数转换

<p align="center"><img src="http://latex.codecogs.com/gif.latex?\\x^{*}=\log_{10}{^x)}/\log_{10}{^(max)}" title="对数函数转换" /></p>
  
+ 反正切函数转换

<p align="center"><img src="http://latex.codecogs.com/gif.latex?\\x^{*}=atan(x)*\pi" title="反正切函数" /></p>

参考
----------------
+ [在网页中显示数学公式](http://www.it165.net/DWeb/html/201410/2942.html)
+ [Markdown输入数学公式](http://ttang.name/2014/05/04/markdown-and-mathjax/)
+ [数据归一化和两种常用的归一化方法](http://www.cnblogs.com/chaosimple/archive/2013/07/31/3227271.html)
+ [数据的标准化](http://webdataanalysis.net/data-analysis-method/data-normalization/)

