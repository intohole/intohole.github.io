---
layout: post
title: jupyter note book 使用 
tags: [ml]
---


安装
----------
```
sudo pip install jupyter
```

运行
-------
```
jupyter notebook
```

远程登陆
------

+ 生成配置文件
   ```shell
   $jupyter notebook --generate-config
   ```
+ 生成密码
  ```python 
    In [1]: from notebook.auth import passwd
    In [2]: passwd()
    Enter password: 
    Verify password: 
    Out[2]: 'sha1:******************'
  ```
+ 修改默认配置文件
  ```shell
  $vim ~/.jupyter/jupyter_notebook_config.py
  ```
  - 修改如下配置项
    ```
    c.NotebookApp.ip='*'
    c.NotebookApp.password = u'sha1:****刚才复制的那个密文'
    c.NotebookApp.open_browser = False
    c.NotebookApp.port =8888 #随便指定一个端口
    ```
+ 启动notebook 
  ```jupyter notebook
  ```
+ 远程访问
  浏览器直接访问 远程ip:8888

  - 如果远程访问出现问题，可以使用ssh进行关联端口
    ```shell
    ssh username@address_of_remote -L127.0.0.1:1234:127.0.0.1:8888
    ```
    使用本地浏览器访问 localhost:1234可以访问notebook了

问题整理
---------
+ Unexpected error while saving file: Untitled.ipynb [Errno 13] Permission denied: '/home/xxxx/.local/share'
   ```shell
   sudo chmod 777 ~/.local/share/jupyter/
   cd ~/.local/share/jupyter/
   ls
   sudo chmod 777 runtime/
   cd runtime/
   ls
   ``` 
