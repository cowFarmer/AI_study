### 2022.01.04 -
- EXPLORATION
 - 인공지능과 가위바위보하기
 - 가위바위보 분류기 만들기
---
### 후기
제대로 된 딥러닝 프로그램을 만들진 않았지만, flow를 느끼기엔 충분했다.   

---
### 2022.01.06 log

learning.ipynb 추가 --> 모든 코드를 관리하는 파일   
오늘 다시 테스트하니 아래와 같은 결과값이 나오지 않음   
그래서 딥러닝 학습 구간 수정 및 여러 테스트 진행   
하지만 테스트 케이스 돌리자 accuracy가 0.3...~ 만 나옴   
그래서 학습 이미지와 테스트 이미지의 편차를 생각함   

**다음번 수정 예정 - 학습 및 테스트 이미지 흑백으로 편차 줄이기**

---
### 2022.01.04 log
image size를 28x28 >> 56x56으로 키움   
image 학습 데이터를 rock, scissor, paper 각 300EA >> 900EA로 총 2700EA 사용   
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
