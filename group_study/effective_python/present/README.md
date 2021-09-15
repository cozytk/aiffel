# Use `zip` for mutiple iterator
## Better Way 8
*여러 이터레이터에 대해 나란히 루프를 수행하려면 zip을 사용하라*

### 개요

```python
# names와 counts를 동시에 다루고 싶음

names = ['Cecilia', '남궁민수', '毛泽东']
counts = [len(n) for n in names] # [7, 4, 3]
```

- 위의 리스트(이터러블)를 동시에 이터레이션을 하고 싶음

- ※ **이터러블 (Iterable)**

    ### 이터러블

    > 멤버들을 한 번에 하나씩 돌려줄 수 있는 객체

    **예시**

    - 모든 시퀀스 형들 (list, str, tuple etc)
    - 몇몇 비 시퀀스 형들 (dict ...)
    - 파일 객체들, __iter__()나 시퀀스 개념을 구현하는 __getitem__() 메서드를 써서 정의한 모든 클래스의 객체들

    **사용**

    - for 루프
    - zip(), map()

    - 내장 함수 iter()에 인자로 전달되면, 그 객체의 이터레이터를 돌려줌. 이 이터레이터는 값들의 집합을 한 번 거치는 동안 유효
    - 사용할 때, iter()를 호출하거나, 이터레이터 객체를 직접 다룰 필요 없음. for문이 자동으로 루프를 도는 동안 이터레이터를 잡아둘 이름 없는 변수를 만듬

    **레퍼런스**

    [Glossary - Python 3.9.7 documentation](https://docs.python.org/ko/3/glossary.html)

## 가장 긴 이름을 출력해보자!

### Index(range, enumerate)를 활용

- code

    ```python
    longest_name = None
    max_count = 0

    for i in range(len(names)):
        count = counts[i]
        if count > max_count:
            longest_name = names[i]
            max_count = count

    print(longest_name)

    >>>

    'Cecilia'
    ---------------------------------

    longest_name = None
    max_count = 0

    for i, name in enumerate(names):
        count = counts[i]
        if count > max_count:
            longest_name = name
            max_count = count

    print(longest_name)
    ```

**❗문제**

- 시각적으로 잡음이 많음
- 인데스를 사용해 names와 counts의 원소를 찾는 과정이 코드를 읽기 어렵게 만듬
- 배열 인덱스 i를 사용해 배열 원소를 가져오는 연산이 두 번 일어남

    → `count = counts[i]` 등의 연산을 할때 다시 배열의 인덱스로 접근을 해야하니까

- enumerate를 사용하면 약간 나아지지만 이 코드도 여전히 이상적이지는 않음

    나아진다는게 시작적으로 나아진다는 건가

### zip 활용

**zip이란?**

- 둘 이상의 이터레이터를 지연 계산 제너레이터를 사용해 묶어줌
- zip 제너레이터는 각 이터레이터의 다음 값이 들어 있는 튜플을 반환, 이 튜플을 for문에서 바로 언패킹 가능

지연 계산 제너레이터

→ Lazy Evaluation. 계산의 결과 값이 필요할 때까지 계산을 늦추는 기법.

- code

    ```python
    longest_name = None
    max_count = 0

    for name, count in zip(names, counts):
        if count > max_count:
            longest_name = name
            max_count = count

    print(longest_name)

    names.append('Rosalind')
    for name, count in zip(names, counts):
        print(name)
    ```

**✅ 장점**

- 인덱스를 사용해 여러 리스트의 원소에 접근하는 코드보다 훨씬 깔끔
- 자신이 감싼 이터레이터 원소를 하나씩 소비

    → 메모리를 다 소모해서 프로그램이 중단되는 위험 없이 아주 긴 입력도 처리할 수 있음.

    → 너무 많은 메모리를 다룰 시 RAM에 꽉찰 수 있는데, 제너레이터를 사용해서 개선 

❗**문제 (예외 사항)**

- 입력 데이터의 길이가 서로 다를 때 자신이 감싼 이터레이터 중 어느 하나 끝날 때까지 튜플을 내놓음

    → 출력은 가장 짧은 입력의 길이

### zip_longest

**zip_longest?**

- itertools 내장 모듈
- 존재하지 않는 값을 자신에게 전달된 fillValue로 대신함. 디폴트 fillValue는 None.

- code

    ```python
    import itertools
    for name, count in itertools.zip_longest(names, counts):
        print(f'{name}: {count}')
    ```

**⏰ When(언제)**

- zip에 전달한 리스트의 길이가 같다고 보장하지 않을 때


# Allocate none and write doc-string for mutable default argument
## Better Way 24

*None과 독스트링을 사용해 동적인 디폴트 인자를 지정하라*

### 세 줄 요약

1. 디폴트 인자 값은 그 인자가 포함된 함수 정의가 속한 모듈이 로드되는 시점에 단 한 번만 평가된다.

    → 동적인 값(mutable), ({}, [], datatime.now() 등)의 경우 이상한 동작이 일어날 수 있음.

2. 동적인 값을 가질 수 있는 키워드 인자의 디폴트 값을 표현할 때는 **None**을 사용하라. 그리고 함수의 독스트링에 실제 동적인 디폴트 인자가 어떻게 동작하는 문서화해두라.
3. 타입 애너티이션을 사용할 때도 None을 사용해 키워드 인자의 디폴트 값을 표현하는 방식을 적용할 수 있다.

### 개요

- 나는 지금 키워드 인자의 값으로 정적으로 정해지지 않는 타입(mutable)의 값을 쓰고 싶음
- 그 중에서, 로그 메시지와 시간을 함께 출력하고 싶음.
- 기본적으로 함수 호출 시간을 포함하길 원함

🤔 **가정**

함수가 호출될 때마다 디폴트 인자가 재계산됨

```python
from time import sleep
from datetime import datetime

def log(message, when=datetime.now()):
    print(f'{when}: {message}')

log('안녕!')
sleep(0.1)
log('다시 안녕!')
```

- log가 최소 0.1초 간격으로 차이가 나겠지?

```python
>>>

2021-09-14 14:38:07.987458: 안녕!
2021-09-14 14:38:07.987458: 다시 안녕!
```

**❗문제**

- 함수가 정의되는 시점에 datetime.now()가 단 한번만 호출되기 때문에 타임스탬프가 항상 같음.
- 디폴트 인자의 값은 모듈이 로드(load)될 때 단 한번만 평가, 보통 프로그램이 시작할 때 모듈을 로드

✅ **해결 (일반적인 관례)**

디폴트 값으로 None을 지정하고 실제 동작을 독스트링에 문서화!

```python
def log(message, when=None):
    """메시지와 타임스탬프를 로그에 남긴다.

    Args:
        message: 출력할 메시지.
        when: 메시지가 발생한 시각(datetime).
            디폴트 값은 현재 시간이다.
    """
    if when is None:
        when = datetime.now()
    print(f'{when}: {message}')

log('안녕!')
sleep(0.1)
log('다시 안녕!')
>>>
# 타임 스탬프가 달라짐!!!

2021-09-14 14:38:14.250035: 안녕!
2021-09-14 14:38:14.355220: 다시 안녕!
```

디폴트 인자 값으로 None을 사용한 것은 인자가 가변적인(mutable) 경우 특히 중요!

🤔 **가정**

나는 JSON 데이터로 인코딩된 값을 읽고 싶음, 데이터 디코딩에 실패하면 디폴트로 빈 딕셔너리를 반환할거야!

```python
import json

def decode(data, default={}):
    try:
        return json.loads(data)
    except ValueError:
        return default

foo = decode('잘못된 데이터')
foo['stuff'] = 5
bar = decode('또 잘못된 데이터')
bar['meep'] = 1
print('Foo:', foo)
print('Bar:', bar)

assert foo is bar
```

**예상**

키와 값이 하나뿐인 서로 다른 딕셔너리

```python

Foo: {'stuff': 5, 'meep': 1}
Bar: {'stuff': 5, 'meep': 1}
```

**문제**

- datetime.now의 경우와 같음.

✅ **해결**

디폴트 값으로 None을 지정하라!

```python
def decode(data, default=None):
    """문자열에로부터 JSON 데이터를 읽어온다

    Args:
        data: 디코딩할 JSON 데이터.
        default: 디코딩 실패시 반환할 값이다.
            디폴트 값은 빈 딕셔너리다.
    """
    try:
        return json.loads(data)
    except ValueError:
        if default is None:
            default = {}
        return default

foo = decode('잘못된 데이터')
foo['stuff'] = 5
bar = decode('또 잘못된 데이터')
bar['meep'] = 1
print('Foo:', foo)
print('Bar:', bar)
assert foo is not bar
```

```python
Foo: {'stuff': 5}
Bar: {'meep': 1}
```

타입 애너테이션과 정적분석을 사용해도 잘 작동.

```python
from typing import Optional

def log_typed(message: str,
              when: Optional[datetime]=None) -> None:
    """메시지와 타임스탬프를 로그에 남긴다.

    Args:
        message: 출력할 메시지.
        when: 메시지가 발생한 시각(datetime).
            디폴트 값은 현재 시간이다.
    """
    if when is None:
        when = datetime.now()
    print(f'{when}: {message}')
```

※ Optional[type]

- 괄호로 받은 type과 None만 받겠다!

### 결론

mutable한 인자를 매개변수로 받을 때는 None을 디폴트 인자로 지정하라!

### 더 나아가기 :왜 동적인 매개변수는 문제가 생길까?

```python
import json

def decode(data, default={}):
    try:
        return json.loads(data)
    except ValueError:
        return default

>>>

def decode(data, default=None):
    """문자열에로부터 JSON 데이터를 읽어온다

    Args:
        data: 디코딩할 JSON 데이터.
        default: 디코딩 실패시 반환할 값이다.
            디폴트 값은 빈 딕셔너리다.
    """
    try:
        return json.loads(data)
    except ValueError:
        if default is None:
            default = {}
        return default
```

- 사실 이 예시는 default에 None을 할당해주어 장땡이 아니라, except문 안에서 if 구문을 사용해서 default를 새로 할당해준 것이 주효.

```python
import json

def decode(data, default={}):
    try:
        return json.loads(data)
    except ValueError:
       if default is {}:
            default = {}
        return default
```

- 위의 코드도 정상적으로 작동 합니다!

```python
Foo: {'stuff': 5}
Bar: {'meep': 1}
```

Q**, 어떤 일이 일어날까요?**

```python
#%%

def foo(var=[]):
    var.append(1)
    return var
foo()
foo()
foo()
```

- 정답

    ```python
    >>>
    [1]
    [1, 1]
    [1, 1, 1]
    ```

    **정리**

    디폴트 매개변수로 한 번 할당된 변수 var이 함수 scope(지역) 안에 보존되고 있음.

    내부 변수를 바꿀 수 있는 mutable한 자료형은 이런 문제가 발생.

    값을 바꾸려면 새로운 객체를 생성해야하는 immutable은 X

### 추가 ) 영현님

```python
import json

def decode(data, default={}):
    try:
        return json.loads(data)
    except ValueError:
        return default

>>>

def decode(data, default=None):
    """문자열에로부터 JSON 데이터를 읽어온다

    Args:
        data: 디코딩할 JSON 데이터.
        default: 디코딩 실패시 반환할 값이다.
            디폴트 값은 빈 딕셔너리다.
    """
		if default is None:
			default = data
			data = 'default what u wants'
			return deault
    try:
        return json.loads(data)
    except ValueError:
        if default is None:
            default = {}
        return default
```

- 매개변수를 두개 활용, default를 내가 원하는 것으로 지정