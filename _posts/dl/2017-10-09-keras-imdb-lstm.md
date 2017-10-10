---
layout: default
tags: [dl]
city: 杭州
title: keras IMDB LSTM例子注释
---

```python
"""在IMDB情感分析任务数据训练lstm模型。
相对简单／更加快速的方法,例如tf-idf+(LogReg)逻辑回归,这个数据集太小对于lstm模型
记住:

- RNNs是有技巧的, 比如训练数据大小选择是非常重要的,
损失(loss)还有优化函数(optimizer)是严格的，等等诸如此类
Some configurations won't converge.

- LSTM loss decrease patterns during training can be quite different
from what you see with CNNs/MLPs/etc.
'''
from __future__ import print_function

from keras.preprocessing import sequence
from keras.models import Sequential
from keras.layers import Dense, Embedding
from keras.layers import LSTM
from keras.datasets import imdb

# 选择训练属性大小
max_features = 20000
# 截断训练数据
maxlen = 80 
# 训练大小
batch_size = 32

print('Loading data...')
# 选择词频大于max_features的特征

(x_train, y_train), (x_test, y_test) = imdb.load_data(num_words=max_features)
print(len(x_train), 'train sequences')
print(len(x_test), 'test sequences')

print('Pad sequences (samples x time)')
# 将训练数据进行截断，如果训练数据长度大于maxlen，则进行截断操作；如果不足默认补0
x_train = sequence.pad_sequences(x_train, maxlen=maxlen)
x_test = sequence.pad_sequences(x_test, maxlen=maxlen)
print('x_train shape:', x_train.shape)
print('x_test shape:', x_test.shape)

print('Build model...')
model = Sequential()
model.add(Embedding(max_features, 128))
model.add(LSTM(128, dropout=0.2, recurrent_dropout=0.2))
# 全联接网络，使用sigmod来做激活函数，用于二分类问题
model.add(Dense(1, activation='sigmoid'))

# try using different optimizers and different optimizer configs
model.compile(loss='binary_crossentropy',
              optimizer='adam',
              metrics=['accuracy'])

print('Train...')
model.fit(x_train, y_train,
          batch_size=batch_size,
          epochs=15,
          validation_data=(x_test, y_test))
score, acc = model.evaluate(x_test, y_test,
                            batch_size=batch_size)
print('Test score:', score)
print('Test accuracy:', acc)
```
参考文章
------------
+ [keras lstm例子](https://github.com/fchollet/keras/blob/master/examples/imdb_lstm.py)
