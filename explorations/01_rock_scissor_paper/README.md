데이터셋 문헌 읽어보자

- 교차검증

```python
n_channel_1=32
n_channel_2=64
n_channel_3=128
n_dense_1=256
n_dense_2=64
n_train_epoch=10

model=keras.models.Sequential()
'''
model.add(keras.layers.experimental.preprocessing.RandomFlip("horizontal", 
                                                 input_shape=(28, 
                                                              28,
                                                              3)))
'''
#model.add(keras.layers.experimental.preprocessing.RandomRotation(0.1))
#model.add(keras.layers.experimental.preprocessing.RandomZoom(0.1))|
#model.add(keras.layers.experimental.preprocessing.Rescaling(1./255))
model.add(keras.layers.Conv2D(n_channel_1, (3,3), activation='relu', input_shape=(28,28,3)))
model.add(keras.layers.MaxPool2D(2,2))
model.add(keras.layers.Conv2D(n_channel_2, (3,3), activation='relu'))
model.add(keras.layers.MaxPooling2D((2,2)))
#model.add(keras.layers.Dropout(0.3))
model.add(keras.layers.Conv2D(n_channel_3, (3,3), activation='relu'))
model.add(keras.layers.MaxPooling2D((2,2)))
model.add(keras.layers.Flatten())
#model.add(keras.layers.Dense(n_dense_1, activation='relu'))
model.add(keras.layers.Dense(n_dense_2, activation='relu'))
model.add(keras.layers.Dropout(0.3))
model.add(keras.layers.Dense(3, activation='softmax'))
                                  
model.compile(optimizer='adam',
             loss='sparse_categorical_crossentropy',
             metrics=['accuracy'])

model.fit(x_train_norm, y_train, epochs=n_train_epoch)n_channel_1=32
n_channel_2=64
n_channel_3=128
n_dense_1=256
n_dense_2=64
n_train_epoch=10

model=keras.models.Sequential()
'''
model.add(keras.layers.experimental.preprocessing.RandomFlip("horizontal", 
                                                 input_shape=(28, 
                                                              28,
                                                              3)))
'''
#model.add(keras.layers.experimental.preprocessing.RandomRotation(0.1))
#model.add(keras.layers.experimental.preprocessing.RandomZoom(0.1))|
#model.add(keras.layers.experimental.preprocessing.Rescaling(1./255))
model.add(keras.layers.Conv2D(n_channel_1, (3,3), activation='relu', input_shape=(28,28,3)))
model.add(keras.layers.MaxPool2D(2,2))
model.add(keras.layers.Conv2D(n_channel_2, (3,3), activation='relu'))
model.add(keras.layers.MaxPooling2D((2,2)))
#model.add(keras.layers.Dropout(0.3))
model.add(keras.layers.Conv2D(n_channel_3, (3,3), activation='relu'))
model.add(keras.layers.MaxPooling2D((2,2)))
model.add(keras.layers.Flatten())
#model.add(keras.layers.Dense(n_dense_1, activation='relu'))
model.add(keras.layers.Dense(n_dense_2, activation='relu'))
model.add(keras.layers.Dropout(0.3))
model.add(keras.layers.Dense(3, activation='softmax'))
                                  
model.compile(optimizer='adam',
             loss='sparse_categorical_crossentropy',
             metrics=['accuracy'])

model.fit(x_train_norm, y_train, epochs=n_train_epoch)
```