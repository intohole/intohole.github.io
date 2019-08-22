---
layout: post  
title: java 反射&泛型相关技巧
city: 上海   
tags: [lan]  
---

+ 获得继承的接口泛型的类型代码
```java
Type[] types = listener.getClass().getGenericInterfaces();
ParameterizedType parameterized = (ParameterizedType) types[0];
Class<T> clazz = (Class<T>) parameterized.getActualTypeArguments()[0];
```
+ 获得类泛型接口实现
```java
 Class<T> tClass = (Class<T>)((ParameterizedType)getClass().getGenericSuperclass()).getActualTypeArguments()[0];
```
