---
layout: post
tags: [open]
title: 创建githubpage	
city: 杭州 
---



=========
+ [fork](https://github.com/intohole/intohole.github.com)
+ 更改你的工程名称->setting->Repository name
	+ ${username}.github.com
+ 清空你的工程下面内容
    + sh \_clean.sh
+ 更改CNAME下面的站点名称,更改为你的网址，或者忽略掉
+ 更改\_config.yml文件选项
    + 请详细看[\_config.yml配置](https://github.com/intohole/intohole.github.com/blob/master/README.md)
+ 编写内容在\_post/ 目录下

	
		---
   		layout: post
   		tags: [你在_config.yml配置的标签]
   		title: 标题 
   		city: 城市 
   		---
		
		markdown编写网页内容


