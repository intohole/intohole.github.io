---
layout: default  
title: sublime插件安装   
city: 北京   
tags: [tech]  
---


sublime 
------------------


+ 安装
    + 在sublime中调出console [ctrl + `] ，粘贴如下代码，回车
    
:::code     
        
        import urllib.request,os; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); open(os.path.join(ipp, pf), 'wb').write(urllib.request.urlopen( 'http://sublime.wbond.net/' + pf.replace(' ','%20')).read())


+ 添加插件
    * 安装插件后，按下[ctrl + shrift + p]组合件 ， 键入 Install Package后，稍等片刻，会出现package名称

插件推荐
-----------------
+ Markdown Editing
    * 一款可以在sublime编辑时，同时展示效果的插件

+ Markdown Preview
    * 可以在浏览器中，查看markdown效果的插件，蛮赞的！

+ SublimeCodeIntel
    * 代码提示功能！写python，写代码必备

+ Python PEP8 AutoFormat
    * 快捷键[ctrl + alt + 8],python 自动代码格式化！代码看起来很简洁的样子

+ ConvertToUTF8
    * 转换文件编码，使用方式 [ctrl + shrift + p],ConvertToUTF8 选择编码方式

+ Git 
    * git版本控制器


快捷键
----------------

:::code      
    
        Ctrl+Shift+P：打开命令面板
        Ctrl+P：搜索项目中的文件
        Ctrl+G：跳转到第几行
        Ctrl+W：关闭当前打开文件
        Ctrl+Shift+W：关闭所有打开文件
        Ctrl+Shift+V：粘贴并格式化
        Ctrl+D：选择单词，重复可增加选择下一个相同的单词
        Ctrl+L：选择行，重复可依次增加选择下一行
        Ctrl+Shift+L：选择多行
        Ctrl+Shift+Enter：在当前行前插入新行
        Ctrl+X：删除当前行
        Ctrl+M：跳转到对应括号
        Ctrl+U：软撤销，撤销光标位置
        Ctrl+J：选择标签内容
        Ctrl+F：查找内容
        Ctrl+Shift+F：查找并替换
        Ctrl+H：替换
        Ctrl+R：前往 method
        Ctrl+N：新建窗口
        Ctrl+K+B：开关侧栏
        Ctrl+Shift+M：选中当前括号内容，重复可选着括号本身
        Ctrl+F2：设置/删除标记
        Ctrl+/：注释当前行
        Ctrl+Shift+/：当前位置插入注释
        Ctrl+Alt+/：块注释，并Focus到首行，写注释说明用的
        Ctrl+Shift+A：选择当前标签前后，修改标签用的
        F11：全屏
        Shift+F11：全屏免打扰模式，只编辑当前文件
        Alt+F3：选择所有相同的词
        Alt+.：闭合标签
        Alt+Shift+数字：分屏显示
        Alt+数字：切换打开第N个文件
        Shift+右键拖动：光标多不，用来更改或插入列内容
        鼠标的前进后退键可切换Tab文件
        按Ctrl，依次点击或选取，可需要编辑的多个位置
        按Ctrl+Shift+上下键，可替换行


##参考
* [Sublime Text 3 常用插件以及安装方法](http://www.cnsecer.com/460.html)
* [Sublime Text 3能用支持的插件推荐](http://www.tuicool.com/articles/qEFJrm)
* [Sublime Text 使用介绍/全套快捷键及插件推荐](http://www.ithome.com/html/soft/31560.htm)