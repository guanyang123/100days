100days
===========
day41 深度学习基础Python，TensorFlow和Keras
```python
X = X/255.0
model = Sequential()
model.add(Conv2D(256, (3, 3), input_shape=X.shape[1:]))
model.add(Activation('relu'))
model.add(MaxPooling2D(pool_size=(2, 2)))
# 这将我们的三维特征图转换为一维特征向量
# 全连接层输出维度为64
model.add(Dense(64))
model.add(Dense(1))
model.add(Activation('sigmoid'))
model.compile(loss='binary_crossentropy',
              optimizer='adam',
              metrics=['accuracy'])
model.fit(X, y, batch_size=32, epochs=3, validation_split=0.3)
```
