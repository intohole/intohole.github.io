---
layout: post  
tags: [tech,go]   
title:	Go学习目录整理    
city: 北京 
---



Go资料整理
-----------------
+ [gopl-zh](https://github.com/golang-china/gopl-zh)
	+ 一个中文教程 ， github上的 ， 感觉很靠谱， 多学习之
+ [awesome-go](https://github.com/avelino/awesome-go)
	+ github上每门语言，都有这样一个列表，方便找到你需要的帅气packages
+ [Go安装](https://github.com/astaxie/build-web-application-with-golang/blob/master/zh/01.1.md)
	+ windows/linux
	

		
			./make.bash: line 121: : No such file or directory
			错误issue: https://github.com/moovweb/gvm/issues/155 

			git clone git@github.com:golang/go.git
			git checkout go1.4
			cd src
			./all.bash
			vi ~/.bashrc
			export GOROOT_BOOTSTRAP="go代码目录最上层路径"
			export PATH=$GOROOT_BOOTSTRAP:${PATH}
			git checkout go1.5.2
			cd src
			./all.bash
		
			
		
+ [Go语言学习资料与社区索引](https://github.com/Unknwon/go-study-index)
+ [Go语言编程 - 微盘](http://vdisk.weibo.com/s/fBR30EqBY7a)
	+ 微盘的pdf
+ [Go并发编程 - Csdn](http://download.csdn.net/detail/xing8831925/8818215)