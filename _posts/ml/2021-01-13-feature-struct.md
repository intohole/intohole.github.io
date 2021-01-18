---
layout: post
title:  特征服务架构图
tags: [ml]
city: 南京 
---


背景
--------
算法服务中很多时候需要访问各种在线特征或者离线统计特征进行算法模型运算，而如何构建一个通用且能简单易用算法框架尤为重要，避免算法工程师将精力浪费再无用的重复造轮子中;

架构图
---------
![特征架构图](/images/feature-project-struct.png)

参考
--------
+ [外卖排序系统特征生产框架](https://tech.meituan.com/2016/12/09/feature-pipeline.html)
