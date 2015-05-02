---
layout: post  
title: Ubuntu install Jekyll  
city: 北京   
tags: [tech,web]  
---


Ubuntu安装Jekyll
---------------
+ [Jekyll网站](http://jekyll.bootcss.com/)              

            #ruby 环境安装
            sudo apt-get install ruby1.9.3   
            sudo apt-get install ruby1.9.1-dev
            sudo apt-get install nodejs  
            #安装gem
            sudo apt-get install rubygems
            #更换软件源
            #列出原有软件源，都是国外
            sudo gem source -l 
            #删除原有source
            sudo gem source -remove * #以上所有名称  
            #添加taobao软件源
            sudo gem source -a  -a http://ruby.taobao.org/
            #安装 jekyll
            sudo gem install jekyll 
            #安装 markdown 依赖  
            sudo gem install rdiscount


Ubuntu使用Jekyll    
--------------------------

            jekyll build 
            jekyll server




参考网站
----------------

+ [Ubuntu下搭建Jekyll环境](http://bo.moioi.com/2013/ubuntu-jekyll/)
+ [ubuntu 搭建 Jekyll环境](http://www.07net01.com/program/239652.html)
+ [搭建一个免费的，无限流量的Blog----github Pages和Jekyll入门](http://www.ruanyifeng.com/blog/2012/08/blogging_with_jekyll.html)
+ [StrayBirds](https://github.com/minixalpha/StrayBirds)
+ [我的jekyll配置和修改](http://blog.javachen.com/2013/08/31/my-jekyll-config/)
