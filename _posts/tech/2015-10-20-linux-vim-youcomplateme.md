---
layout: post
tags: [tech,vim]  
title: Vim安装YouComplateMe
city: 北京
---



插件安装
================
+ 插件管理
	
	{% highlight python %}
			
			假设已经安装vim 插件管理器vundle 
			vim ~/.vimrc添加插件
			Plugin 'Valloric/YouCompleteMe
			在任意打开vim中，执行命令行:BundleInstall
		
	{% endhighlight %}	

+ 安装顺序
	
	{% highlight python %}
		
		git clone https://github.com/Valloric/YouCompleteMe
		当出现这个提示时：
			git submodule update --init --recursive
		ycmd没有安装正确 ， 如果执行上述命令不成功；直接安装ycmd
		1. git clone https://github.com/Valloric/ycmd
		2. sudo apt-get install build-essential cmake python-dev
		3. git submodule update --init --recursive
		4. cmake 安装 ，因为本人系统是ubuntu，安装版本低于要求版本，从官网下载一个解压包，解压后bin目录，移动到sudo mv bin/* /usr/bin/
		5.	./build.py --clang-completer --omnisharp-completer --gocode-completer
		7. cd ../YouCompleteMe 
		8. ./install.py --clang-completer
		
	{% endhighlight %}


+ 我的.vimrc设置

	{% highlight python %}

		set ts=4
		set expandtab
		set nocompatible
		filetype off
		set rtp+=~/.vim/bundle/Vundle.vim
		call vundle#rc()
		Plugin 'gmarik/Vundle.vim' " let Vundle manage Vundle
		Plugin 'scrooloose/nerdtree'
		Plugin 'majutsushi/tagbar'
		Plugin 'klen/python-mode'
		Plugin 'wesleyche/SrcExpl'
		Plugin 'Valloric/YouCompleteMe'

		filetype plugin indent on
		syntax on
		nmap <silent> <F4> :TagbarToggle<CR>
		let g:tagbar_ctags_bin='/usr/bin/ctags'

	{% endhighlight %}


参考
-------------
+ [YouComplateMe](https://github.com/Valloric/YouCompleteMe)
+ [ycmd](https://github.com/Valloric/ycmd)
+ [cmake3.4](https://cmake.org/download/)
+ [Vim自动补全神器：YouCompleteMe](http://blog.jobbole.com/58978/)
+ [Vim自动补全神器：YouCompleteMe | 重点文章](http://blog.jobbole.com/58978/)