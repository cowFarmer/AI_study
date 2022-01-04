### 2022.01.04
- EXPLORATION
 - 인공지능과 가위바위보하기
 - 가위바위보 분류기 만들기
---
### How?\n
image size를 28x28 >> 56x56으로 키움\n
image 학습 데이터를 rock, scissor, paper 각 300EA >> 900EA로 총 2700EA 사용

\n
```python
n_channel_1=64
n_channel_2=256
n_dense=256
n_train_epoch=12

model=keras.models.Sequential()
model.add(keras.layers.Conv2D(n_channel_1, (3,3), activation='relu', input_shape=(28,28,3))) # rgb라 1 -> 3으로 바꿈
model.add(keras.layers.MaxPool2D(2,2))
model.add(keras.layers.Conv2D(n_channel_2, (3,3), activation='relu'))
model.add(keras.layers.MaxPooling2D((2,2)))
model.add(keras.layers.Flatten())
model.add(keras.layers.Dense(n_dense, activation='relu'))
model.add(keras.layers.Dense(3, activation='softmax')) # 최종 분류기의 Class수이다. 주먹, 가위, 보 3종류이므로 10 -> 3

```
해당 값을 넣어 모델을 학습 시켰음
결과는 **10/10 - 0s - loss: 1.0028 - accuracy: 0.6967**
