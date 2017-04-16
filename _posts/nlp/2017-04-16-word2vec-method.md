---
layout: post
title: word2vec转换为sentencevec方法 
tags: [nlp]
city: 杭州 
---


句子向量一些方法
===================
+ Doc2vec:通过训练模型直接获得句子向量，但不足点，doc2vec需要离线训练，句子变成向量是一次性过程，添加新的句子需要重新训练过程
+ WordVector平均方法：word2vec训练获得词向量，通过累加平均向量的方法得出句子向量
+ WordVector平均方法通过TFIDF:word2vec训练获得词向量，但累加的时候将每个词*TFIDF后累加在一起，得到句子向量,但通过实验得到，效果不明显；
+ WordVector最大向量方法:word2vec训练获得词向量，句子中每个词合并时候取最大值，效果通过一些demo是有效果的 



