---
layout: post
title: Phantomjs 安装使用
tags: [tech]
city: 南京
---


# PhantomJS 安装与配置指南
PhantomJS 是一个无头浏览器，常用于网页自动化、网络监测、网页截屏以及无界面测试等。
## 安装步骤
1. 使用pip安装PhantomJS：
   ```bash
   pip install phantomjs
   ```
2. 如果需要手动下载PhantomJS，可以从以下地址下载：
   [PhantomJS 官方下载](https://phantomjs.org/download)
3. 解压下载的文件：
   ```bash
   tar -xvf phantomjs*.tar
   ```
## 常见问题解决
如果在安装过程中遇到“status code 127”的问题，特别是在CentOS系统上，您可能需要安装一些依赖项。
### 在CentOS上解决安装问题
1. 安装`fontconfig`：
   ```bash
   sudo yum install fontconfig
   ```
2. 安装中文字体：
   ```bash
   sudo yum install bitmap-fonts bitmap-fonts-cjk
   ```
3. 安装字体相关的依赖包：
   ```bash
   sudo yum groupinstall "fonts" -y
   ```
4. 刷新字体缓存：
   ```bash
   fc-cache
   ```
## 配置环境变量
1. 添加PhantomJS的执行路径到`.bashrc`文件：
   ```bash
   vim ~/.bashrc
   ```
   在文件中添加以下行：
   ```bash
   export PATH=$PATH:/你所在的路径/phantomjs/bin
   ```
2. 执行以下命令使更改生效：
   ```bash
   source ~/.bashrc
   ```
3. 将PhantomJS变成可执行文件：
   ```bash
   chmod 777 /你所在的路径/bin/phantomjs
   ```
按照这些步骤操作，应该能够成功安装并配置PhantomJS。


## 样例代码
```python
from selenium import webdriver

driver = webdriver.PhantomJS(executable_path='/你所在的路径/bin/phantomjs')
driver.get("https://mbd.baidu.com/newspage/data/landingsuper?context=%7B%22nid%22%3A%22news_10167933854751916862%22%7D&n_type=-1&p_from=-1")

print(driver.page_source)

driver.quit()
```
python3 xxx.py


```
