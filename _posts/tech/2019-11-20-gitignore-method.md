---
layout: post
title: gitignore写法 
tags: [tech]
city: 上海 
---

只允许某些文件类型可以输入
---------
```
*
!*/
!*.py
!*.ipynb
*-checkout.ipynb
```
+ 使用方法
   - 在根目录里面创建 .gitignore文件，编辑文件
+ 禁止某些输入 
  - 前面加上 !
+ gitignore优先级
  - 从上到下一次匹配，所以 !*.ipynb 允许所有ipynb后缀名称文件,但是排除-checkout.ipynb文件

