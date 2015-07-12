---
layout: post
tags: [tech,nodejs]
title: Ubuntu 安装nodejs 
city: 北京
---

Ubuntu 安装nodejs
====================



方法
----------------------
+ apt-get 安装方式


:::code 
        
        sudo add-apt-repository ppa:chris-lea/node.js
        sudo apt-get update
        sudo apt-get install nodejs
        sudo apt-get install nodejs
        sudo apt-get install npm
        #node js 0.6.14版本很低 


+ 源码安装

:::code 
    
        #从git上下载git源码
        #git clone git://github.com/joyent/node.git
        #查看下github上分支,查找最新分支
        $git checkout 最新分支名称 #本人使用的时候 v0.12.5-release 
        $./configure
        $make 
        $make install 
        $sudo ln -s /usr/local/bin/node /usr/bin/node
        $sudo ln -s /usr/local/bin/npm /usr/bin/npm

express安装
-------------
        
        $sudo npm install -g express-generator



参考 
-------------
+ [准备Nodejs开发环境Ubuntu](http://blog.fens.me/nodejs-enviroment/)
+ [搭建 Node.js 开发环境](https://github.com/alsotang/node-lessons/tree/master/lesson0)
+ [Ubuntu 14.04下搭建Node.js开发环境](http://www.linuxidc.com/Linux/2014-12/110983.htm)
+ [Ubuntu下搭建Node.js+express web开发框架](http://developer.51cto.com/art/201202/315938.htm)
+ [Installing Node.js via package manager](https://github.com/joyent/node/wiki/Installing-Node.js-via-package-manager#arch-linux)
+ [express官网-开始](http://www.expressjs.com.cn/guide.html)