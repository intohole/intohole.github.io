---
layout: post
title: anconda jupyter多环境
tags: [tech]
city: 上海
---

安装环境
---------


+ [Anaconda3的安装和使用](https://www.jianshu.com/p/b627671ca1f3)
+ [Anconda3 Linux下载地址](https://www.anaconda.com/distribution/#linux)
+ 使用wget命令,下载Anconda3安装包
```shell
    bash Anaconda3-5.2.0-Linux-x86_64.sh
    # 按照提示输入，否则可以一直enter
```


Anconda基础命令行
------


```shell
  conda info --envs # 查看虚拟环境
  conda create -n 虚拟环境名称 python=python版本号 #(eg:python=python2.7)
  conda activate 虚拟环境名称  #激活对应的虚拟环境
  conda detivate  # 返回上一个虚拟环境
  conda install 包名 # 例如:jieba
```


Anconda启动jupyter
---------
+ 启动jupter
```shell
  jupyter notebook --port ${port} --ip ${ip}
```
+ 添加jupyter密码
```shell
  jupyter notebook passwd
```


Anconda启动多环境(python2/python3)
---------
+ 创建环境
```shell
   conda create -n python27 python=python2.7 
   conda create -n pytyhon3 python=python3.7.4
```
+ 在每个虚拟环境上安装ipykernel
```shell
   conda install ipykernel
```   
+ 激活对应环境
```shell
   source activate 环境名称
```
+ 添加环境python到notebook内核中
```shell        
    python -m ipykernel install --user --name 虚拟环境名称 --display-name "展示名称"
```
+ 启动notebook
```shell
   jupyter notebook 
```


参考
--------
+ [jupyter notebook选择conda环境](https://blog.csdn.net/u011606714/article/details/77741324)



