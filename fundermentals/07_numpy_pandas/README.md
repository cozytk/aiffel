# 개요

- list, numpy 사용법
- dictionary, pandas 사용법
- 이미지 데이터 numpy 배열로 저장
- 통계 데이터 계산

# 몰랐던 것

### 표준편차

- 표준편차는 모집단 - 1 로 나누어야함.

### 리스트

- 파이썬 리스트는 element들이 연속된 메모리 공간에 배치됨

### numpy

- `np.array()` 에 문자열을 하나라도 넣어주면 모든 원소가 문자열이됨
- `dtype` 을 통하여 넘파이 배열 내부의 원소 타입 확인 가능
- 덧셈 연산을 할때 한 축이라도 맞으면 원소의 길이를 늘려서 덧셈
- PIL.Image.Image 라는 랩퍼 클래스를 상속받은 타입을 가진 `img` 는 리스트를 상속받지 않았지만 __array_interface__라는 속성의 정의되어 있음. 그래서 Pillow 라이브러리는 Numpy ndarray로 변환 가능
- data augmentation(데이터의 개수를 늘릴 때) 이미지 조작이 많이 사용됨

### pandas

- numpy 기반에서 개발 됨
- 데이터베이스처럼 데이터를 합치고 관계연산 수행 가능

### series

- Series의 인덱스는 인덱스이면서 dictionary의 key 같은 역할
- 객체와 인덱스 각각의 `name` 속성이 있음

### EDA

- 데이터를 탐색하는 것
- 

# 궁금한 것

동적 타입 언어인 파이썬의 리스트가 어떻게 연속된 메모리 공간에 배치될 수가 있지

- 실제로 id를 찍어보면 다른 위치에 저장이 되는 것으로 알고 있음

PIL.Image.Image 라는 랩퍼 클래스를 상속받은 타입을 가진 `img` 는 리스트를 상속받지 않았지만 __array_interface__라는 속성의 정의되어 있음. 그래서 Pillow 라이브러리는 Numpy ndarray로 변환 가능

```
rope : 1coins/pcs * 2pcs = 2 coins
apple : 2coins/pcs * 10pcs = 20 coins
torch : 2coins/pcs * 6pcs = 12 coins
gold coin : 5coins/pcs * 50pcs = 250 coins
knife : 30coins/pcs * 1pcs = 30 coins
arrow : 1coins/pcs * 30pcs = 30 coins

treasure_box = {'rope': {'coin': 1, 'pcs': 2},
                'apple': {'coin': 2, 'pcs': 10},
                'torch': {'coin': 2, 'pcs': 6},
                'gold coin': {'coin': 5, 'pcs': 50},
                'knife': {'coin': 30, 'pcs': 1},
               	'arrow': {'coin': 1, 'pcs': 30}
               }
treasure_box['rope']
```