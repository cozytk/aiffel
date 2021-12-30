### 베이지안 머신러닝 모델

- 데이터를 통해 파라미터 공간의 확률 분포를 학습
- 모델 파라미터를 고정된 값이 아닌 불확실성(uncertainty)을 가진 확률 변수로 보는 것, 데이터를 관찰하면서 업데이트되는 값으로 보는 것이 핵심 아이디어

### prior(사전 확률)

데이터를 관찰하기 전 파라미터 공간에 주어진 확률 분포

### likelihood(기능도, 우도)

prior 분포를 고정시킨다면, 주어진 파라미터 분포에 대해서 우리가 갖고 있는 데이터가 얼마나 그럴듯한지 계산할 수 있음, 이것을 나타내는 값
p(X=x∣θ) 즉, 파라미터의 분포 p(θ)p(θ)가 정해졌을 때 x

### MLE(maximum likelihood estimation)

- 데이터들의 likelihood 값을 최대화하는 방향으로 모델을 학습시키는 방법

### posterior(사후 확률)

데이터 집합 X가 주어졌을 때 파라미터의 분포

데이터를 관찰한 후 계산되는 확률

데이터 포인트의 개수는 유한하기 때문에 데이터가 따르는 확률 분포 $p(X)$는 우리가 정확하게 알 수 없음

애초에 머신러닝의 목표가 $p(X)$를 직접 구할 수가 없으니까 모델 파라미터 $\theta$를 조절해가면서 간접적으로 근사

posterior를 직접 계산해서 최적은 $\theta$ 값을 찾는 것이 아니라, prior와 likelihood에 관한 식으로 변형한 다음, 그 식을 최대화하는 파라미터 $\theta$를 찾는 것

### MAP (maximum a posteriori estimation)

- posterior를 최대화하는 방향으로 모델을 학습시키는 방법

확률 곱셈정리 - [[https://blog.naver.com/mykepzzang/220834900088](https://blog.naver.com/mykepzzang/220834900088)]([https://blog.naver.com/mykepzzang/220834900088](https://blog.naver.com/mykepzzang/220834900088)) 베이지안 이론 - [[https://bioinformaticsandme.tistory.com/47](https://bioinformaticsandme.tistory.com/47)]([https://bioinformaticsandme.tistory.com/47](https://bioinformaticsandme.tistory.com/47)) 베이지안 이론2 - [[https://ratsgo.github.io/statistics/2017/07/01/bayes/](https://ratsgo.github.io/statistics/2017/07/01/bayes/)]([https://ratsgo.github.io/statistics/2017/07/01/bayes/](https://ratsgo.github.io/statistics/2017/07/01/bayes/)) MLE MAP 대략적 설명 블로그 - [[https://darkpgmr.tistory.com/62](https://darkpgmr.tistory.com/62)]([https://darkpgmr.tistory.com/62](https://darkpgmr.tistory.com/62)) - [[https://jkim777.tistory.com/7](https://jkim777.tistory.com/7)]([https://jkim777.tistory.com/7](https://jkim777.tistory.com/7)

순정 상태의 ubuntu 터미널이 나오고 또 홈디렉토리에 /work 폴더에 먼저 하신 카뎃분들 작업도 볼 수 있더라구요