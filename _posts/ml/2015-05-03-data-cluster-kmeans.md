---
layout: post
title: 聚类算法 Kmeans
city: 北京
tags: [ml]
---

ＫMeans　聚类算法
================
+ 流程

	{% highlight c %}
    伪代码:
	seeds = random(data , k)
	#seeds cluster center　
	#ｋ　　cluster counts
	repeat:
		for data in datas;    
			find data min distance in seeds and update data cluster = k 
		update cluster center 
      	until cluster doesn't change(center change rate small than you set diff quota)
	{% endhighlight %}
        
Kmeans难点
------------
+ ｋ值确定
	+ [canopy](https://github.com/intohole/moodstyle/blob/master/moodstyle/clusterutils/canopy.py)一种粗聚类算法，只要确定两个阈值！
+ 距离公式选择
	+ 欧几得距离
	+ 马氏距离
	+ 闵可夫斯基距离
	+ 汉明距离
	+ 广义Jaccard系数
	+ Jaccard系数
+ 数据处理
	+ [数据归一化](/2015/01/12/data-normalization.html)

KMeans家族
---------

<span></span>

+ KMeans++: 用权重方式随机生成质心，让质心在距离上．离的远一些，让聚类更加随机，避免在点密集部分，过分集中
+ Kmedios:　更新质心，不是类内数据平均值，而是类中离所有数据，距离最近的数据，作为新的中心，让聚类效果更加有代表性！



参考
-----------
+ [浅谈Kmeans聚类](http://www.cnblogs.com/easymind223/archive/2012/10/30/2747178.html)
+ [基本Kmeans算法介绍及其实现](http://blog.csdn.net/qll125596718/article/details/8243404)
+ [数据点间距离公式](http://blog.csdn.net/july_2/article/details/18559337)

