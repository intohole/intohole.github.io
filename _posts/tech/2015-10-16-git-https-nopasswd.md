---
layout: post
title: Git Https 免登陆
city: 北京
tags: [tech,git]
---


Git Https 免登录
=================

+ 方法1
	
	:::code 
		
		创建文件：
			touch ~/.git-credentials
			vim ~/.git-credentials

		添加内容
			https://{username}:{passwd}@github.com
		Git全局选项配置
			git config --global credential.helper store
			git config credential.helper 'cache --timeout=3600' #设置密码生存时间，可忽略
			git config --global credential.helper store --file ~/.my-credentials #设置自己 .git-credentials文件
		vim ~/.gitconfig
			[credential]
    			helper = store

+ 方法2
	
	:::code 
		
		创建文件
			touch ~/.netrc
			vim ~/.netrc
		添加内容
			machine git.baidu.com
			login 用户名
			password 用户密码
		Git全局选项配置
			git config --global credential.helper store
			git config credential.helper 'cache --timeout=3600' #可以忽略此设置
		vim ~/.gitconfig
			[credential]
    			helper = store

参考
----------
[Git-工具-凭证存储](https://git-scm.com/book/zh/v2/Git-%E5%B7%A5%E5%85%B7-%E5%87%AD%E8%AF%81%E5%AD%98%E5%82%A8)