### 판별 모델링

- 입력된 데이터셋을 특정 기준에 따라 분류하거나, 특정값을 맞추는 (회귀) 모델
- 입력받은 데이터를 어떤 기준에 대해 판별하는 것이 목표

### 생성 모델링

- 학습한 데이터셋과 비슷하면서도 기존에는 없던 새로운 데이터셋을 생성하는 모델
- 없던 데이터를 생성해내는 것이 목표

### DeepComposer에서 Generator(생성자)와 Discriminator(판별자)

- Generator는 오케스트라처럼 직접 음악을 연주하여 만들어내는 모델
- Discriminator는 오케스트라가 연주한 음악을 평가하여 오케스트라가 만들어 내는 음악이 점점 좋아지게 만드는 지휘자의 역할

### Pix2Pix

- 간단한 이미지를 입력할 경우 실제 사진처럼 보이도록 바꿔줌
- 단순화된 이미지와 실제 이미지가 쌍을 이루는 데이터셋으로 학습을 진행

  **논문**

[https://arxiv.org/pdf/1611.07004.pdf](https://arxiv.org/pdf/1611.07004.pdf)

### CycleGAN

- 한 이미지와 다른 이미지를 번갈아 가며 Cyclic하게 변환
- Pix2Pix는 한 방향 변환, CycleGAN은 양뱡향 변환.
- Pix2Pix는 그림과 사진의 쌍으로 이루어진 데이터셋 필요, CycleGAN 필요 X

### Neural Style Transfer

- 이미지의 스타일을 변환
- 전체 이미지의 구성을 유지하고 싶은 Base Image와 입히고 싶은 스타일이 담긴 Style Image 두 장을 활용해 새로운 이미지를 만들어 냄
- `Neural` = 신경망, 딥러닝 기술을 사용했다는 뜻