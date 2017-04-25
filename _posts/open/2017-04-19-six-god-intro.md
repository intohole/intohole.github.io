---
layout: post
tags: [open]
title:	正文抽取算法
city: 杭州 
---


精小正文提取工具
=========

项目背景
-------
+ 抓取网页的时候需要我们来编码抽取网页正文或者其他信息；而我们想把爬虫做大的时候发现，我们大部分人力都消耗在各种提取上，繁复提取规则
+ 优点：线性时间、不建DOM树、与HTML标签无关
+ [sixgod](https://github.com/intohole/sixgod)      

{%hightlighter python%}		
		from vampire.htmlextract import HtmlExtract
		import requests
		html = requests.get('http://www.fabao365.com/fangchan/167193/')  
    	html.encoding="utf-8"
		ex = HtmlExtract()
		print ex.get_text(html.text)
{%endhighlight%}


+ 主要思想：[基于行块分布函数的通用网页正文抽取](https://wenku.baidu.com/view/2b5c9793daef5ef7ba0d3cb5.html)

参考资料
-----------
+ [通用网页正文抽取](http://www.oschina.net/p/cx-extractor)
