## 목표

- Tensorflow V2의 개요와 특징을 파악한다.
- Tensorflow V2의 3가지 주요 API 구성방식을 이해하고 활용할 수 있다.
- GradientTape를 활용해 보고 좀더 로우레벨의 딥러닝 구현방식을 이해한다

## 개요

**PyTorch**

Tensorflow API와 달리 **철저히 파이써닉**하고 **직관적인 API 설계**와 **쉬운 사용법**

**Tensorflow V2**

pyTorch가 가진 장점을 대부분 흡수

Keras라는 pyTorch와 아주 닮은 API를 Tensorflow의 표준 API로 삼음

Google이 가진 분산 환경을 다루는 엄청난 기술력과 결합하여 더욱 강력한 딥러닝 프레임워크로 진화

### 딥러닝 모델

forward propagation 방향의 모델만 설계하면 그 모델의 gradient를 사전에 미리 구해둘 수 있음

### tf V1 문제

- 기본적으로 사용하기가 어려움.
- 코드도 길고 지저분
- 파이써닉하지 않기 때문에 구현 방식 자체가 난이도가 높음
- 무엇보다도, 그래프를 다 만들어놓고 돌려봐야 비로소 모델 구성 시의 문제가 드러남,
- 문제가 발생했을 때 해결하기가 너무나 어렵고 복잡했기 때문입니다.

### Eagar Mode

딥러닝 그래프가 다 그려지지 않아도 얼마든지 부분 실행 및 오류검증이 가능

→ Tensorflow `Eager Mode` 에서 적극 수용

### 강화학습 또는 GAN하면 GredientTape 필수