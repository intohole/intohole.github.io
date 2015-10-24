---
layout: post
tags: [tech,python]
title: python日志模块logging
city: 北京
---

python 日志模块
==============



为什么我们使用log工具
-------------------
+ 为什么不用print
	-	你可以用这原始模块来输出，但是你会面临如下困境的时候，你该怎么办

		{% highlight c %}

			1.	想将日志保存在文件中
			2.	想将文件既输出终端又输出到文件
			3.	想输出各种程序输出
			4.	想规范自己的日志格式
			5.	想输出某个等级以上日志信息时

		{% endhighlight %}

+ logging 特性
	
	{% highlight python %}
	
		import logging
		logging.debug('debug info')
		logging.info('info')
		logging.warning('warning')
		logging.error('error')
		logging.critical('critical')
		
		日志等级 critical > error > warning > info > debug > noset 
	
		import logging
		
		#logging基础设置
		logging.basicConfig(level=logging.DEBUG,
                format='%(asctime)s %(filename)s[line:%(lineno)d] %(levelname)s %(message)s',
                datefmt='%a, %d %b %Y %H:%M:%S',
                filename='myapp.log',
                filemode='w')
    
		logging.debug('This is debug message')
		logging.info('This is info message')
		logging.warning('This is warning message')

	{% endhighlight %}
	
	





参考
----------
[python 的日志logging模块学习](http://www.cnblogs.com/dkblog/archive/2011/08/26/2155018.html)
[python 简单封装](https://github.com/intohole/b2/blob/master/b2/log2.py)