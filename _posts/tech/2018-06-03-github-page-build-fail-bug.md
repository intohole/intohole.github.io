---
layout: post
title: GithubPage Build Fail 查找过程 
tags: [tech]
city: 杭州 
---


GithubPage build Fail 查找过程
---------

环境
-----
+ Ubuntu16.04


定位问题步骤
-------
+ github page 没有给出明确的问题所在
    - 建本地环境
       - ruby 环境升级到2+
       - jekyll 安装
    - 结果
       - 环境问题没有搞定
+ 查看错误信息
    - ![github page build错误信息](/images/github-build-error.png)
    - 解决方法
        - 
            ```
                cd ${GITHUB_PAGE_HOME}/_posts/ 
                for i in `ls`;do echo ${i}" "`cat ${i} | head -n 6 | tail -n 1`; done
            ```
        - 发现标签字段有问题
            ```
                tags: [,xxx]
                tags: [12,13/14]
                -> tags: [xxx]
            ```
