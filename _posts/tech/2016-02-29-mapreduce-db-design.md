---
layout: post
title: 关于心中一个database的想法
city: 北京
tags: [tech]
---

一些想法
=========
hadoop 集群数据库思想
-------
	
+ 对所有数据按照第一列数据，进行全局排序（mapreduce）
	+ 大数据全量排序实现思路
	

			1.  对数据全量扫描，随机抽取链接（每n条抽取一条），得到一个索引A
			2.	将索引A按照从大大小排序
			3.  mapreduce程序，读入索引A，将所有数据按照索引文件进行分化（二分法），找到对应格子号，格子号\t数据输出到reduce里面
			4.  reduce是有序的文件
			5.  对reduce进行首尾（可以多个位置），选出索引文件B（最终的索引文件），mapreuce读入数据/单机读入，可以读取指定part数据了
