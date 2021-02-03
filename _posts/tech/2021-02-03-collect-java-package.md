---
layout: post
title: JAVA 好的包裹收集
tags: [tech]
city: 南京
---


背景
---------
JAVA & 算法日常开发，站在巨人的肩膀，最大化自己效率，把自己的精力，用在核心地方（重复造轮子，精力过于分散;功能迭代需要大量失败），为此收集日常使用中见到的好的包


+ fastjson
   - alibaba出品
   - ```java
     JSONObject json = JSONObject.parseObject("{\"name\":\"hello world!\"}");
     System.out.println(json);
     ```
