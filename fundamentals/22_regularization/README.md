### 목표

- Regularization(정칙화)와 Normalization(정규화) 구분
- L1 regularization과 L2 regulrarization 차이 설명
- Lp norm, Dropout, Batch Normalization 학습

### Regularization

- 오버피팅을 해결하기 위한 방법 중 하나
- L1, L2, Dropout, Batch Normalization 등
- Linear Regression이 L2 Norm과 관련

### Normalization

- 데이터의 형태를 좀 더 의미 있게, 혹은 트레이닝에 적합하게 전처리
- 데이터의 scale 범위가 크면 노이즈가 생성되기 쉬움, Overfitting이 일어나기 쉬움
- 학습을 더 빨리 시킬 수 있고, local optimum에 빠질 가능성 줄어듦
- Scale이 너무 커서 값의 분포 범위가 넓어지면 값 정하기가 힘들어짐

### L1 regulariazation (Lasso)

![스크린샷 2021-11-01 오전 10.21.10.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/dce96cfd-76c6-4753-8b8e-1f0604943511/스크린샷_2021-11-01_오전_10.21.10.png)

![스크린샷 2021-11-01 오전 10.21.19.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/586afcb1-a20f-431a-a2bd-b3a310840b77/스크린샷_2021-11-01_오전_10.21.19.png)

위의 부분이 없다면 Linear Regression과 동일

**X가 2차원 이상인 여러 컬럼 값이 있는 데이터일 때 실제 효과**를 볼 수 있습니다.

### L2 regularization

L1 Regularization에서는 몇 개의 축에서 $\beta$값을 0으로 보냄.

하지만, L2 regularization은 $\beta^2$이므로 원의 형태로 나타나게 됨 

→ 0에 가지는 않고 0에 가깝게 감. 또한 제곱이 들어가 있기 때문에 절댓값으로 L1 Norm보다 수렴이 빠름

### L1 & L2 비교

**L1 Regularization**

가중치가 적은 벡터에 해당하는 계수를 0으로 보내면서 **차원 축소와 비슷한 역할**을 하는 것이 특징

**L2 Regularization**

0이 아닌 0에 가깝게 보내지만 제곱 텀이 있기 때문에 **L1 Regularization보다는 수렴 속도가 빠르**다는 장점

### Norm

**vector norm**

p가 무한대일때 가장 큰 숫자 출력

**matrix norm**

p=1, 컬럼의 합이 가장 큰 값 출력

p=무한, 로우의 합이 가장 큰 값 출력

### `apply()`

- 매개변수로 함수를 주고, 모든 열이 함수에 적용될 수 있도록

**예시**

`target_df['species'] = target_df['species'].apply(converter)`

### `concat()`

- 열 기준으로 합쳐줌

### 특정 행값에 해당하는 행의 특정 열 값 추출하기

```python
X = [iris_df['petal length (cm)'][a] for a in iris_df.index if iris_df['species'][a]=='virginica']
Y = [iris_df['sepal length (cm)'][a] for a in iris_df.index if iris_df['species'][a]=='virginica']
```

### Dropout

**fully connected architecture**

- 모든 뉴런들이 연결되어 있음
- 드롭아웃이 나오면서 확률적으로 랜덤하게 몇 가지의 뉴럴만 선택하여 정보를 전달하는 과정
- 확률적으로 버리면서 전달하는 기법
- 오버피팅을 막는 Regularization lyaer중 하나
- 확률 높이면, 제대로 전달되지 않으므로 학습이 잘되지 않고, 확률을 너무 낮추는 경우 fully connected layer
- fully connected layer에서 오버피팅이 생기는 경우에 주로 dropout 추가
- 좋은 데이터셋에다 하면 오히려 악영향 미침

### Batch Normalization

- gradient vansihing, explode 문제를 해결하는 방법
- 분모에 $\epsilon$(앱실론)이 추가
- normalize 과정에서 gradient가 사라지거나(vanishing), 폭등하는(explode) 것을 막을 수 있음
- $**\epsilon**$(앱실론) 제외하면 ****기존의 z-score 로 normalize 하는 과정과 같지만, 추가하는 것만으로도 오버피팅이나 학습이 잘 되지 않는 것 막음
- batch normalization 추가하면 **좀 더 빠르게 정확도 상승, loos 함수의 감소도 빨라짐.**
- batch normalization으로 인해 이미지가 정규화되면서 좀 더 고른 분포를 가지기도 하고,  $\epsilon$(앱실론) 부분으로 인해 안정적인 학습이 가능

### 더 나아가기

- 개수를 0으로 보낸다는 것 이해

Linear Regression에서는 모든 컬럼의 가중치를 탐색하여 구하는 반면, L1 Regularization에서는 총 13개 중 7개를 제외한 나머지의 값들이 모두 0임을 확인할 수 있습니다.

- 22-3 코드 이해하기, L2규제 구현 따라오기
- **예를 들어, A=[1,1,1,1,1]*A*=[1,1,1,1,1] , B=[5,0,0,0,0]*B*=[5,0,0,0,0] 의 경우 L1-norm은 같지만, L2-norm은 같지 않습니다.**