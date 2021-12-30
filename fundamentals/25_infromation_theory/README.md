### 학습 목표

- 정보이론
- Entropy, Cross Entropy, KL divergence

### 학습 내용

- Information Content
- Entropy
- Kullback Leibler Divergence
- Cross Entropy Loss
- Decision Tree와 Entropy

### 정보 이론

- 추상적인 '정보'라는 개념을 정량화하고 정보의 저장과 통신을 연구

### Information Content

**정보를 정량적으로 표현하기 위해 필요한 세 가지 조건**

1. 일어날 가능성이 높은 사건은 정보량이 낮고, 반드시 일어나는 사건에는 정보가 없는 것이나 마찬가지
2. 일어날 가능성이 낮은 사건은 정보량이 높음
3. 두 개의 독립적인 사건이 있을 때, 전체 정보량은 각각의 정보량을 더한 것과 같음

**정의**

$I(x) = -log_bP(x)$

### Entropy

- 특정 확률분포를 따르는 사건들의 정보량 기댓값

### For Discrete Random Variables

$H(X) = -\sum_{i = 1}^{n}p_ilogp_i$

- 시행마다 각각 다른 사건이 일어날때 엔트로피는 최대값을 가짐
- .. 균등할수록 엔트로피값은 증가함

For Continuous Random Variables

X가 이산 확률 변수일 때 엔트로피는 위와 같이 정보량에 확률을 각각 곱해서 모두 더한 값으로 정의됩니다. XXX가 연속적인 값을 갖는 연속 확률 변수일 때는 유한합 대신 적분의 형태로 정의합니다. 확률 변수 XXX의 확률 밀도 함수가 p(x)p(x)p(x)일 때 엔트로피는 다음과 같습니다.

h(X)=−∫p(x)logp(x)dx

연속 확률 변수의 엔트로피를 이산 확률 변수와 구분하여 **미분 엔트로피**(differential entropy)라고 부르기도 합니다.

:cl