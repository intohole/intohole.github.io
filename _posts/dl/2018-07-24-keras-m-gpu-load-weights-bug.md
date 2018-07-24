---
layout: default
tags: [dl]
city: 杭州
title: keras多显卡训练及预测需要注意点
---
+ 训练代码
  - 
    ```python
        
    from keras.utils import multi_gpu_model
    # 0 < gpus <= 你真实含有的gpu数量 
    parallel_model = multi_gpu_model(model, gpus=8)
    # 进行编译
    parallel_model.compile(loss='categorical_crossentropy',
                       optimizer='rmsprop')

    # fit 方法会在8个gpu上分布运行，就是将数据一个batch里面的数据平均分到8个gpu上
    # 由于batch_size = 256,每块gpu有256/8数据在运行
    parallel_model.fit(x, y, epochs=20, batch_size=256)
    ```


+ 问题
   - ValueError: You are trying to load a weight file containing 3 layers into a model with 1 layers.
     ```python
       #加载模型的时候，先将模型创建起来
       model = create_model()
       model = multi_gpu_model(model , gpus = 8) 
     ```
   - Check failed: work_element_count > 0 (0 vs. 0)
     ```python
        tensorflow==1.8.0 -> tensorflow==1.7.0
       
     ```
+ 参考资料
   - [Check failed: work_element_count > 0 (0 vs. 0) #521](https://github.com/matterport/Mask_RCNN/issues/521)
   - [Keras同时用多张显卡训练网络](https://vpn.dayin.com/web/1/http/0/www.leadai.org/article/133)
   - [Keras FAQ：常见问题](http://keras-cn.readthedocs.io/en/latest/for_beginners/FAQ/#GPU)
