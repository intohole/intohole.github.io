---
layout: default
title: git过滤不提交文件
city: 北京
tags: [tech]
---

git 过滤不提交文件方法
==========
+ 针对单一工程排除文件，这种方式会让这个工程的所有修改者在克隆代码的同时，也能克隆到过滤规则，而不用自己再写一份，这就能保证所有修改者应用的都是同一份规则；

        在工程根目录下建立.gitignore文件，将要排除的文件或目录 写到.gitignore这个文件中
  
+ 全局设置排除文件，这会在全局起作用，只要是Git管理的工程，在提交时都会自动排除不在控制范围内的文件或目录。
        
        建立 .gitignore文件，把要排除的文件写进去。
        git config --global core.excludesfile .gitignore，


+  单个工程设置排除文件，在工程目录下找到.git/info/exclude，但是不会提交到管理系统，作为本地过滤文件，不适合集体编码习惯

参考
-------------
+ [Git 过滤文件，控制上传](http://blog.csdn.net/hustpzb/article/details/8649545)