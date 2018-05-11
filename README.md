博客
=========


博客基于框架
-----------
+ jekyll
+ linux系统下: 先运行sh \_clean.sh

博客配置
------------
+ \_config.yml
	+ 支持多说账号
		
```python		
	comments: 
	provider: duoshuo
	duoshuo:
		short_name: 账户名
```	
	+ 设置多个分类
		
```python		
	indexs:
		- site: 首页
		  url: index.html
	# site 分类名称 , index.html 页面地址 ;请参考我的博客设置
```
	+ 404页面设置

```python
			page_404:
 				refresh_time: 7
 				btns:
   					- info: 看看我的Github
     			      url: https://github.com/intohole
   					- info: 看看首页
                      url: /index.html
```
	+ 代码的格式设置，请参考

```python			
	code_type: manni
```
	+ 介绍页面设置


```python
	resume:
		Desc:
			- info: "Java python shell c and etc... "
			- info: "Mail：aihai2800 AT 126 Dot com"

		Jobs:
			- 
				type: Github
				name: intohole
				url: https://github.com/intohole
			- 
				type: Weibo
				name: 看似大男人的小男人
				url: http://weibo.com/1152049780 
```
    + type 配置参考 http://www.fontawesome.com.cn/ 图标 ， 可以省略fa- 开头，目前集成这个
    + name 显示文字
    + url 跳转链接

+ CNAME
	+ 设置自己网站的重定向，参照我的设置，请各位在清空这个设置后使用我的网页

+ 谢谢 
	+ git@github.com:JeremyWei/jeremywei.github.com.git
