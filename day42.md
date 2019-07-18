100days
===========
day42 深度学习基础Python，TensorFlow和Keras
```python
import tensorflow as tf
import time
from tensorflow.keras.datasets import cifar10
from tensorflow.keras.preprocessing.image import ImageDataGenerator
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Dense, Dropout, Activation, Flatten
from tensorflow.keras.layers import Conv2D, MaxPooling2D
from tensorflow.keras.callbacks import TensorBoard
import pickle


NAME = "Cats-vs-dogs-64x2-CNN"
pickle_in = open("C:/Users/86178/PycharmProjects/untitled/venv/X.pickle","rb")
X = pickle.load(pickle_in)
pickle_in = open("C:/Users/86178/PycharmProjects/untitled/venv/X.pickle","rb")
y = pickle.load(pickle_in)

X = X/255.0
model = Sequential()
model.add(Conv2D(256, (3, 3), input_shape=X.shape[1:]))
model.add(Activation('relu'))
model.add(MaxPooling2D(pool_size=(2, 2)))
model.add(Flatten())
# 全连接层输出维度为64
model.add(Dense(64))
model.add(Dense(1))
model.add(Activation('sigmoid'))

# 保存模型的训练数据logs/NAME，然后由TensorBoard读取。
tensorboard = TensorBoard(log_dir="logs/{}".format(NAME))
model.compile(loss='binary_crossentropy',
              optimizer='adam',
              metrics=['accuracy'],
              )
model.fit(X, y,
          batch_size=32,
          epochs=3,
          validation_split=0.3,
          callbacks=[tensorboard])
          
          
          
```
