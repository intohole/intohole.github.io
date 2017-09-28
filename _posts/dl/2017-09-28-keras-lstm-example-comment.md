---
layout: default
tags: [dl]
city: 杭州
title: keras LSTM例子注释
---

```python
这是用Nietzsche的著作生成文本的例子代码。

生成文本至少需要20轮迭代。

运行这个脚本建议在gpu上，因为循环神经网络需要很大计算量的。

如果你想使用新的文本数据运行这个脚本，请确认数据集至少100k字符，大于1m最好

'''

from __future__ import print_function
from keras.models import Sequential
from keras.layers import Dense, Activation
from keras.layers import LSTM
from keras.optimizers import RMSprop
from keras.utils.data_utils import get_file
import numpy as np
import random
import sys
# 下载文本数据集 ， 我下载出现问题 ， 手动下载后将文件放入到文件夹下 ， 直接运行
path = get_file('nietzsche.txt', origin='https://s3.amazonaws.com/text-datasets/nietzsche.txt')
text = open(path).read().lower()
print('corpus length:', len(text))

# 这个得到字符词典 ， 类似 : [a,b,c...]
chars = sorted(list(set(text)))
print('total chars:', len(chars))
# 得到字符到序号 词典；因为网络输入要求是整数
char_indices = dict((c, i) for i, c in enumerate(chars))
# 得到序号到字符 词典；网络输出是数字
indices_char = dict((i, c) for i, c in enumerate(chars))

# 切割文本最大数目
maxlen = 40
step = 3
sentences = []
next_chars = []
for i in range(0, len(text) - maxlen, step):
    sentences.append(text[i: i + maxlen])
    next_chars.append(text[i + maxlen])
print('nb sequences:', len(sentences))

print('Vectorization...')
# 输入向量化；
# X -> (句子长度,每次切割长度,字符大小) 将输入每个位置按照字符都进行了编码 one-hot 类似 三维数组，在最后一维上进行one-hot编码
X = np.zeros((len(sentences), maxlen, len(chars)), dtype=np.bool)
# X -> y 输入向量对应下一个字符向量编码 
y = np.zeros((len(sentences), len(chars)), dtype=np.bool)
for i, sentence in enumerate(sentences):
    for t, char in enumerate(sentence):
        X[i, t, char_indices[char]] = 1
    y[i, char_indices[next_chars[i]]] = 1


# 搭建lstm网络 
print('Build model...')
model = Sequential()
# 
model.add(LSTM(128, input_shape=(maxlen, len(chars))))
model.add(Dense(len(chars)))
model.add(Activation('softmax'))

optimizer = RMSprop(lr=0.01)
model.compile(loss='categorical_crossentropy', optimizer=optimizer)


def sample(preds, temperature=1.0):
    # helper function to sample an index from a probability array
    preds = np.asarray(preds).astype('float64')
    preds = np.log(preds) / temperature
    exp_preds = np.exp(preds)
    preds = exp_preds / np.sum(exp_preds)
    probas = np.random.multinomial(1, preds, 1)
    return np.argmax(probas)

# train the model, output generated text after each iteration
for iteration in range(1, 60):
    print()
    print('-' * 50)
    print('Iteration', iteration)
    model.fit(X, y,
              batch_size=128,
              epochs=1)

    start_index = random.randint(0, len(text) - maxlen - 1)

    for diversity in [0.2, 0.5, 1.0, 1.2]:
        print()
        print('----- diversity:', diversity)

        generated = ''
        sentence = text[start_index: start_index + maxlen]
        generated += sentence
        print('----- Generating with seed: "' + sentence + '"')
        sys.stdout.write(generated)

        for i in range(400):
            x = np.zeros((1, maxlen, len(chars)))
            for t, char in enumerate(sentence):
                x[0, t, char_indices[char]] = 1.

            preds = model.predict(x, verbose=0)[0]
            next_index = sample(preds, diversity)
            next_char = indices_char[next_index]

            generated += next_char
            sentence = sentence[1:] + next_char

            sys.stdout.write(next_char)
            sys.stdout.flush()
        print()
```
