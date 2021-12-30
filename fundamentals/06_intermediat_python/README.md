# 몰랐던 것

## 스크립트 언어

- 파이썬은 스크립트 언어에 해당
- 수정이 빈번하게 발생하면 수정 후 일일이 컴파일을 해야하는 수고를 덜어줌

    → 수정이 빈번하게 발생하는 부분은 인터프리터 방식이 유리

- 응용 소프트웨어에서 스크립트 언어에 맞는 API를 제공, 응용 소프트웨어와 상호작용하면서 돌아감

## 리스트 컴프리헨션

- 리스트뿐만 아니라 셋 (Set), 딕셔너리 (Dict) 에 대해서도 적용 가능

**이중 for문 구조 리스트 컴프리헨션 예시**

```python
my_list = ['a','b','c','d']

result_list = [(i, j) for i in range(2) for j in my_list]

print(result_list)
>>>

[(0, 'a'), (0, 'b'), (0, 'c'), (0, 'd'), (1, 'a'), (1, 'b'), (1, 'c'), (1, 'd')]
```

## 제너레이터

### `yield`

- 양보하다
- 코드 실행의 순서를 밖으로 양보해줌
- generator object만 반환할 뿐, 원하는 값을 바로 반환하지는 않음

## 멀티프로세싱

**예문**

```python
import multiprocessing
import time

num_list = ['p1','p2', 'p3', 'p4']
start = time.time()

def count(name):
    for i in range(0, 100000000):
        a = 1+2
    print("finish : ", name)
    

if __name__ == '__main__':
    pool = multiprocessing.Pool(processes = 4)
    pool.map(count, num_list)
    pool.close()
    pool.join()

print("time :", time.time() - start)eq
```

**Advice**

- 요즘은 내부 모듈보다 외부 라이브러리를 많이 쓰는 추세임
- 파이토치나 텐서플로우 내부에도 병렬처리 내부 기능이 있음
- ray라는 라이브러리도 핫함. 굉장히 직관적

## 람다

- 익명함수

### `map(f, iterable)`

- 입력으로 함수(f)와 반복 가능한(iterable) 객체(리스트, 튜플 등)를 받습니다.

### pip

- 공개된 패키지만 설치. 공개되지 않거나 직접 만든 패키지는 직접 설치해야함
- pypi.org에서 어떤 패키지가 있는지 찾을 수 있음

    ※ PyPI : THe Python Package Index

### 함수형 프로그래밍

- 데이터 사이언티스트에게 적합
- 효율성, 버그 없는 코드, 병렬 프로그래밍과 같은 장점

**특징**

1. 순수성
    - 함수의 반환값에서 보이지 않는 다른 변경사항을 만드는 부작용이 전혀 없는 함수,
    순수 함수를 사용함
    - 모든 함수의 출력은 입력에만 의존
2. 모듈성
    - 한 가지 작업을 수행하는 작은 함수들로 쪼개어 만듦
3. 디버깅과 테스트 용이성

[Functional Programming HOWTO - Python 3.9.7 documentation](https://docs.python.org/ko/3/howto/functional.html)

---

# 궁금한 것

퍼포먼스가 낮음에도 불구하고 파이썬이 인공지능에 가장 널리 쓰는 언어가 된 이유가 무얼까?

**예상**

- 생각보다 퍼포먼스가 낮지 않음
    - 머신러닝에 필요한 연산들은 퍼포먼스가 비슷하다던가
- 라이브러리가 너무 잘 되어있고, 사용자가 많아 인공지능 언어에서 선점함

- 
- 람다연습

### 이터레이터와 제너레이터

- 인덱스 접근과 이터러블 접근 성능차이
- 리스트 컴프리핸션과 제너레이터 표현식