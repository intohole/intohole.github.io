---
layout: post
titile: 阿里云操作小记
city: 北京
tags: [tech,note]
---

阿里云服务器笔记
===============



添加用户
---------

:::code 	
		
		#useradd -d /home/xxx -m xxx 创建一个用户名为xxx，以/home/xxx为主目录的用户
        #passwd xxx 更改用户密码


命令行提示问题
-----------

:::code		
    
        #sudo vi /etc/passwd 找到xxx用户名，将/bin/sh => /bin/bash
        
添加sudo权限
------------

:::code		
    
        #vim /etc/sudoers 添加 xxx ALL=(ALL) ALL xxx为新增用户名，sudo xxx 提示输入用户密码 ， 输入该用户密码即可
		
        

ssh问题
------------
+ ####Could not open a connection to your authentication agent#### 	

:::code
        
        $eval `ssh-agent`
        $ssh-add ~/.ssh/id_rsa
