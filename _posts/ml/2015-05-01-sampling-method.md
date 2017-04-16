---
title: 抽样方法介绍
tags: [tech,algorithm,ml]
layout: post
city: 北京
---


抽样方法介绍
=================
+ 蓄水池抽样
  
{% highlight python %}          
            k #sample_num
            data #待抽样数据，array
            reservoir_array[k] #抽样数组 
            init reservoir_array in k #计算抽样数组
            for i = k + 1 ; do
                sample_num = randint(0 , i)
                if sample_num < k: #如果随机数落在 [1,k]区域内，则data[sample_num],替换成data[i]
                    reservoir_array[sample_num] = data[i]
            done 
{% endhighlight  %}

+ 流式抽样
        
{% highlight python %} 
        sample_rate #抽样概率
        sample_array #抽样存放数组
        sample_probality = random(0,1)
        for i = 0 ; i < len(data) ;do
            if sample_probality < sample_rate:
                sample_array.append(data[i])
        done 
{% endhighlight  %}

参考
--------------
+ [蓄水池抽样及实现](http://www.cnblogs.com/hrlnw/archive/2012/11/27/2777337.html)