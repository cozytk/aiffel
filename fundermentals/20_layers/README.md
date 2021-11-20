### 목표

- 레이어의 개념을 이해한다.
- 딥러닝 모델 속 각 레이어(Linear, Convolution)의 동작 방식을 이해
- 데이터의 특성을 고려한 레이어를 설계하고, 이를 Tensorflow로 정의하는 법 학습

### 미싱 링크

들어본 적은 있지만 막상 누군가에게 설명하려고 하면 쉽지 않음

### 배우는 것

- Weight의 특성
- 미싱 링크의 진정한 의미
- `Linear` 레이어, `Convolution` 레이어, `Embedding` 레이어, `Recurrent` 레이어를 다룸

## Convolution 레이어

### 사진 필터는 Convolution 연산을 활용

[Image convolution examples](https://aishack.in/tutorials/image-convolution-examples/)

**Stride**

두 세칸씩 이동하며 훑기

**Padding**

입력의 형태를 유지

이미지에서는 인접한 요소간의 인접한 정보가 중요하기 때문에 convolution 레이어를 통해 locality 정보를 온전히 보존

### 궁금한 점

- batch size에 따라 레이어가 어떻게 변화되는가?

### Pooling

Convolution 레이어의 정보 집약 효과 보충

**Convolution 한계**

Convolution Layer의 필터 사이즈를 너무 작게 하면, 유의미한 정보들을 담아내기 너무 작고, stride가 필터와 같으면 파라미터는 줄어들지만 필터 경계선에 걸림

**해결**

filter size가 아닌 receptive filed(수용영역)을 크게 해야함

**왜 힘들게 연산한 3/4를 버릴까? Accuracy 저하 효과는 없는가?**

- trainslational invariance 효과
    - 인접한 영역 중 가장 두드러진 영역 하나를 뽑는 것은 동일한 특징을 안정적으로 잡아낼 수 있는 긍정적 효과
    - object 위치에 대한 오버피팅을 방지하고 안정적인 특징 추출 효과
- Non-linear 함수와 동일한 피쳐 추출 효과
    - 중요한 피쳐만을 상위 레이어로 추출해서 올려줌으로써 결과적으로 분류기의 성능을 증진
- Receptive Filed 극대 효과
    - Convolutional 레이어를 아주 많이 쌓는 것보다는 나음