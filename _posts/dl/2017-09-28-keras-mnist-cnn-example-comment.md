---
layout: default
tags: [dl]
city: 杭州
title: keras MNIST CNN例子注释
---



```python

'''
训练一个卷积神经网络在mnist数据集上.

在12轮迭代后，我们获得99.25%准确率
'''

from __future__ import print_function
import keras
from keras.datasets import mnist
from keras.models import Sequential
from keras.layers import Dense, Dropout, Flatten
from keras.layers import Conv2D, MaxPooling2D
from keras import backend as K

# 每次参加训练的时候数据集大小
batch_size = 128
# 类别数目
num_classes = 10
# 迭代数目
epochs = 12

# 图片长宽大小 
img_rows, img_cols = 28, 28

# 将数据洗牌切割 
(x_train, y_train), (x_test, y_test) = mnist.load_data()

if K.image_data_format() == 'channels_first':
    x_train = x_train.reshape(x_train.shape[0], 1, img_rows, img_cols)
    x_test = x_test.reshape(x_test.shape[0], 1, img_rows, img_cols)
    input_shape = (1, img_rows, img_cols)
else:
    # 训练数据 -> 训练数据大小 图片长度 图片长度 channel数目
    x_train = x_train.reshape(x_train.shape[0], img_rows, img_cols, 1)
    x_test = x_test.reshape(x_test.shape[0], img_rows, img_cols, 1)
    input_shape = (img_rows, img_cols, 1)

# 训练数据转换类型
x_train = x_train.astype('float32')
x_test = x_test.astype('float32')
# 数据进行归一化
x_train /= 255
x_test /= 255
print('x_train shape:', x_train.shape)
print(x_train.shape[0], 'train samples')
print(x_test.shape[0], 'test samples')

# 转换类别向量变成二分类数组 one-hot 编码？
# convert class vectors to binary class matrices
y_train = keras.utils.to_categorical(y_train, num_classes)
y_test = keras.utils.to_categorical(y_test, num_classes)

# 建立模型
model = Sequential()
# Conv2D
# filters = 32 32个卷积核
# kernel_size 指定卷积窗口大小 
# activation 激活函数

model.add(Conv2D(32, kernel_size=(3, 3),
                 activation='relu',
                 input_shape=input_shape))
# 64个卷积核
model.add(Conv2D(64, (3, 3), activation='relu'))
# 做pooling操作 2,2 -> 1
model.add(MaxPooling2D(pool_size=(2, 2)))
# dropout为了避免网络过拟合
model.add(Dropout(0.25))
model.add(Flatten())
# 全联接
# Dense 全联接 
# units 128 输出序列长度 
# activation relu 激活函数
model.add(Dense(128, activation='relu'))
# Dropout 失效网络
model.add(Dropout(0.5))
# softmax多分类
model.add(Dense(num_classes, activation='softmax'))
# loss 损失函数 交叉熵
# optimizer 优化函数 
model.compile(loss=keras.losses.categorical_crossentropy,
              optimizer=keras.optimizers.Adadelta(),
              metrics=['accuracy'])
# 训练模型
model.fit(x_train, y_train,
          batch_size=batch_size,
          epochs=epochs,
          verbose=1,
          validation_data=(x_test, y_test))
score = model.evaluate(x_test, y_test, verbose=0)
print('Test loss:', score[0])
print('Test accuracy:', score[1])

```

参考文章
--------

