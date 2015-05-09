---
layout: post
title: Python Install Packages : Microsoft Visual c++ 9.0 is required
city: 北京
tags: [tech,python]
---


Python Install Packages : Microsoft Visual c++ 9.0 is required
================
+ 症状    
        

        Windows下pip安装包报错：Microsoft Visual C++ 9.0 is required Unable to find vcvarsall.bat
        在Windows7x64下使用pip安装包的时候提示报错：Microsoft Visual C++ 9.0 is required  (Unable to find vcvarsall.bat)

+ 解决方法
	+ [Micorsoft Visual C++ Compiler for Python 2.7](http://www.microsoft.com/en-us/download/details.aspx?id=44266)
	    
		
        msiexec /i /m VcForPython27.msi