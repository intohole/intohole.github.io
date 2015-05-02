---
title: python ssh 远程链接代码  
layout: post  
tags: [tech,python]  
city: 南京
---



使用python  ssh 代码实现
--------------------

{% highlight python %}
        
        #coding=utf-8
        #!/usr/bin/env python
        
        import paramiko
        client = paramiko.SSHClient()
        client.set_missing_host_key_policy(paramiko.AutoAddPolicy())
        #client.connect(ip , 端口 , 用户名 , 用户密码 , 链接超时时间 )
        client.connect('zyl', 22, username='zyl', password='1', timeout=4)
        stdin, stdout, stderr = client.exec_command('ls -l')
        for std in stdout.readlines():
            print std,
        client.close()
{% endhighlight  %}

ssh
------------
一款在linux 远程链接服务器工具  ,python 是一门较容易学习的语言  