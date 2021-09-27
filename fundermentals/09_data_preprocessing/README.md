# 배울 것

- 결측치 (Missing Data)

    → 제거하거나 채워 넣음

- 중복된 데이터

    → 찾아서 제거 가능

- 이상치 (Outlier)

    → 찾고 처리

- 정규화 (Normalization)
- 원-핫 인코딩 (One-Hot Encoding)

    → 범주형 데이터를 사용

- 구간화(Binning)

    → 연속적인 데이터를 구간으로 나눠 범주형 데이터로

# 몰랐던 것

### 전처리의 중요성

- 데이터 분석의 8할은 데이터 전처리이다.

### 결측치 여부 살펴보기

### `df.count()`

- 각 컬럼의 데이터 건수를 반환해줌

    **응용**

    `len(df) - df.count()` : 전체 데이터의 결측치만 출력

### `df.drop(col or row, axis=num)`

- 한 열이나 행을 없애줌

    ex) col 삭제 → `df.drop('col', axis=1)`

### `df.duplicated()`

- 중복된 행이 있는지 찾아줌

    **응용**

    `df[df.duplicated()]` → 중복된 행을 보여줌

### 결측치 해결 방법 (수치형)

1. 특정 값을 지정

    ❗결측치가 많은 경우, 모두 같은 값으로 대체한다면 데이터의 분산이 실제보다 작아짐

2. 평균, 중앙값 등으로 대체 ↔ 최빈값 (범주형)

    ❗1번과 마찬가지

3. 다른 데이터를 이용해 **예측값**으로 대체

    ex) 머신러닝 모델로 2020년 4월 미국의 예측값을 만들고, 이 값으로 결측치를 보완할 수 있습니다.

4. **시계열 특성**을 가진 데이터의 경우 **앞뒤 데이터**를 통해 결측치를 대체

    ex) 기온을 측정하는 센서 데이터에서 결측치가 발생할 경우, 전후 데이터의 평균으로 보완할 수 있습니다.

### 시계열

- 시간에 흐름에 따라 기록된 것

### 중복된 데이터

- id가 중복된 경우 나중에 들어온 값을 남겨야됨
    - 업데이를 하다가 오류가 생긴 경우가 있기 때문

    `df.drop_duplicates(subset=['id'], keep='last')`

### 이상치

- Min-Max Scaling을 해보면 대부분이 0애 수렴하고 이상치만 1에 가까움
- 이런 경우 1을 제거하고 분석

    **anomaly detection**

    현실에서 이상치를 찾는 것

    `**z score` 방법**

    평균을 빼주고 표준편차로 나눔.

    ❗뚜렷한 한계점이 있음

    **IQR(Interquartile range)**

    z-score 방법의 대안

    - 제 3사분위수에서 제 1사분위 값을 뺀 값. 데이터의 중간 50% 범위

        75% 지점 - 25% 지점

    - $Q_1 - 1.5 * IQR$ 보다 왼쪽에 있거나, $Q_3 + 1.5 * IQR$ 보다 오른쪽에 있으면 이상치
- 특정 기준을 넘어서는 데이터에 대해 이상치를 판단
- 기준 작게 → 이상치 판단 데이터 많아짐
- 기준 크게 ⇒ 이상치 판단 데이터 적어짐

### 정규화

**Standardization**

평균은 0, 분산은 1로 변환

`x_standardization = (np-np.mean()) / np.std()`

 **Min-Max Scalling**

최솟값은 0, 최댓값은 1로 변환

`x_min_max = np - np.min() / np.max()` 

- scikit-learn의 `StandardScaler`, `MinMaxScaler` 사용 방법도 있음

    ```python
    from sklearn.preprocessing import import Min
    scaler = MinMaxScaler() #StandardScaler
    scaler.fit_transform(train)
    scaler.fit_transform(test)
    ```

### 원-핫 인코딩

- 카테고리별 이진 특성을 만들어 해당하는 특성만 1, 나머지 0
- `get_dummies` 활용

### 구간화

```python
# ex) bins [0, 2000, 4000, 6000, 8000, 100000], or num (구간을 정확히 나눔)
ctg = pd.cut(df, bins=)

ctg.value_counts().sort_index()
>>>

(1531.93, 2885.0]    27
(2885.0, 4230.0]     24
(4230.0, 5575.0]     21
(5575.0, 6920.0]      6
(6920.0, 8265.0]      7
(8265.0, 9610.0]     15

# ex) q = num (개체의 수가 q로 정확히 나눠지게 자름)
ctg = pd.qcut(df, q=)

ctg.value_counts().sort_index()
>>>

(1539.999, 2618.0]    20
(2618.0, 3544.0]      20
(3544.0, 4648.0]      20
(4648.0, 7068.0]      20
(7068.0, 9610.0]      20
```

# 궁금한 것

### `trade[trade.isnull().any(axis=1)]`

- 이 부분 다시 이해해보기
- 이 그림의 의미는?