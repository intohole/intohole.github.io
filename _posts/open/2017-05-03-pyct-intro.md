---
layout: post
tags: [open]
title: [pyct] python crontab实现	
city: 杭州 
---



[pyct] python crontab实现
========
+ [pyct](https://github.com/intohole/pyct)
+ 接口定义简单
+ 支持crontab字符串的定时时间格式
+ 使用方法
	
	
		from pyct.pyct import PyCt
		c = PyCt()
    		
		def p(*argv , **kw):
        	print "hi"
				
		c.add("* * * * *", p , *[] , **{}) #添加执行命令 ， 现在只支持python函数 , 函数形式类似于这种 def xxx(*argv , **kw):  
		time.sleep(100) # 或者用c.join()

+ 整个实现步骤
	- crontab时间定义字符串的解析
    - [b2](https://github.com/intohole/b2) 多线程池的使用
