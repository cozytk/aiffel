# Day 09

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
 
# Day 08

- Pandas, Matplotlib, Seaborn 이용 그래프 그리기
- 시각화를 해보고 EDA를 하며 인사이트 도출

# 몰랐던 것

### `%matplotlib inline`

IPython에서 사용하는 매직메서드. notebook을 실행한 브라우저에서 바로 그림을 볼 수 있게 해줌.

[ipython 의 매직명령어들](https://studymake.tistory.com/601)

### `plt.plot()`

- plot을 그릴 때는 figure() 객체를 생성하고 add_subplot으로 서브 플롯을 생성해야 함.
- 위 명령으로 그래프를 그리면 matplotlib은 가장 최근의 figure 객체와 서브플롯을 그림. 없으면 서브플롯 하나를 생성

### 범주형 데이터

- 주로 막대 그래프를 사용하여 수치를 요약
- 일반적으로 가로, 세로, 누적, 그룹화된 막대 그래프 사용

### 템플릿

```python
fig = plt.figure() # 새로운 figure 만들어줌
ax1 = add_subplot(1,1,1) or plt.plot(x=,y= ...)
plt.bar or plt.hist or sns.barplot(df, x=, y=) sns.scatterplot etc... #seaborn은 바로 df를 매개변수로 넣어줌
```

# 궁금한 것

```python
>>>

Text(0.5, 1.0, "Yuna's Test Result")
```

시각화를 하고 나오는 값 (0.5, 1.0)의 뜻

### plot 그리기

- plt.show()를 하면 아직 안 넣은 기존에 값이 나오거나 값이 제대로 나오지 않음 어떻게 처리?
- 다 그렸다가 처음부터 다시 그릴때 주의사항

- 한번에 하면 실행이 되고, 쉘을 나눠서 작업하면 plt따로fig따로 그려짐

# Day 07

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

# Day 06

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

- Pandas, Matplotlib, Seaborn 이용 그래프 그리기
- 시각화를 해보고 EDA를 하며 인사이트 도출

# Day 05

# 학습 목표

- 파이썬에서 텍스트 데이터 어떻게 처리하는지
- 파이썬에서 텍스트 파일과 디렉토리에 접근하는 방법
- 텍스트 파일의 종류를 알아보고 각각 다루는 법

# 개념

- 인코딩과 디코딩, 문자열 다루기, 정규 표현식, 파일, 디렉토리, 모듈과 패키지, CSV 파일, XML 파일, JSON 파일

# 알게된 것

### 인코딩과 디코딩

- 변수에 데이터를 할당하면 이 데이터들은 컴퓨터의 주기억장치인 메모리(RAM)에 저장됨

    ↔ 파일에 쓰면 데이터는 보조기억장치인 ROM에 저장됨

- 흔히 UTF-8과 유니코드가 같은 것이라고 혼동하는 경우가 많음
하지만, 유니코드는 오직 한가지 버전만 존재. UTF-8, UTF-16 등은 유니코드로 정의된 텍스트를 메모리에 인코딩하는 방식들
- 파이썬 3부터는 문자열이 무조건 유니코드로 인코딩되므로 해당 텍스트가 인코딩되어 있는지 혹은 디코딩이 되어 있는지만 고려한다면 된다는 것이 포인트

### 원시 문자열

이스케이프 문자를 무시하고 싶을 때 사용하는 것

※ 이스케이프 문자 : \' \" \t \n \\ ...

```python
print('Please don\'t touch it')
print(r'Please don\'t touch it')

>>>
Please don't touch it
Please don\'t touch it
```

### 공백 문자

개행복귀 `\r` : 커서를 맨 앞으로 이동. 커서를 원위치로 복귀.

### 공백 문자 제거하기

```python
#txt = "      공백 문자를 제거해 보아요.      "
txt = "      Strip white spaces.      "
print('[{}]'.format(txt))
print('--------------------------')

#- 양쪽 공백 제거 : strip()
print('[{}]'.format(txt.strip()))
print('--------------------------')

#- 왼쪽 공백 제거 : lstrip()
print('[{}]'.format(txt.lstrip()))
print('--------------------------')

#- 오른쪽 공백 제거 : rstrip()
print('[{}]'.format(txt.rstrip())) 
```

## 정규 표현식

### 정규 표현식 시작

### `import re`

- 파이썬 표준 라이브러리 re

`compile()`

**예시**

```python
#1단계 :  "the"라는 패턴을 컴파일한 후 패턴 객체를 리턴합니다. 
pattern = re.compile("the")    

# 2단계 : 컴파일된 패턴 객체를 활용하여 다른 텍스트에서 검색을 수행합니다.
pattern.findall('of the people, for the people, by the people')
---------------------------------------------------------------
re.findall('the', 'of the people, for the people, by the people')
```

**특수문자, 메타문자 사용 예시**

```python
#- 연도(숫자)
text = """
The first season of America Premiere League  was played in 1993. 
The second season was played in 1995 in South Africa. 
Last season was played in 2019 and won by Chennai Super Kings (CSK).
CSK won the title in 2000 and 2002 as well.
Mumbai Indians (MI) has also won the title 3 times in 2013, 2015 and 2017.
"""
pattern = re.compile("[1-2]\d\d\d")
pattern.findall(text)
>>>
['1993', '1995', '2019', '2000', '2002', '2013', '2015', '2017']

#- 전화번호(숫자, 기호)
phonenumber = re.compile(r'\d\d\d-\d\d\d-\d\d\d\d')
phone = phonenumber.search('This is my phone number 010-111-1111')
if phone:
  print(phone.group())
print('------')
phone = phonenumber.match ('This is my phone number 010-111-1111')
if phone:
  print(phone.group())
>>>
010-111-1111
------

#- 이메일(알파벳, 숫자, 기호)
text = "My e-mail adress is doingharu@aiffel.com, and tomorrow@aiffel.com"
pattern = re.compile("[0-9a-zA-Z]+@[0-9a-z]+\.[0-9a-z]+")
pattern.findall(text)
--------
['doingharu@aiffel.com', 'tomorrow@aiffel.com']
```

### 파일

- `with` 구문. with 구문을 사용하면 open된 객체가 with문이 종료될때 자동으로 close됨

    → 시스템 리소스의 안정성을 위해 `with` 문 활용 권장

**예시**

```python
f = open("hello.txt","w") 
#- open(파일명, 파일모드)
#- 파일을 열고 파일 객체를 반환합니다. 
for i in range(10):
    f.write("안녕")
    #- write() 메소드로 '안녕'을 10번 씁니다.
f.close()
#- 작업이 끝나면 close() 메소드로 닫아줍니다. *필수!

print("완료!")
------------------------------------------
with open("hello.txt", "r") as f:
  print(f.read())
```

### 디렉토리 관련 표준 라이브러리

- sys, ob, glob

### `sys.path`

- 임포트할 때 불러 오는 모듈들이 위치한 경로

**개념**

- 모듈 : 파이썬으로 만든 코드가 들어간 파일 `.py`
- 패키지 : `__init__.py` 가 포함된 폴더. 흔히 라이브러리라 칭함
- pip : 파이썬 패키지 관리자. 파이썬을 설치하면 기본으로 설치
- PyPA : 파이썬 패키지를 관리하고 유지하는 그룹
- PyPI : 파이썬 패키지들의 저장소

### csv 파일 읽고 쓰기 함수들

- open(), write(), 라이브러리 csv, csv.reader(), csv.writer(), csv.writer.writerow()
to_csv(), read_csv()

## XML

- Extensible Markup Language. 다목적 마크업 언어

```xml
<Person>
    <Name>이펠</Name>
    <Age>28</Age>
    <Place>강남</Place>
</Person>
```

### XML 관련 기능 제공

### 파이썬 표준 라이브러리 `ElementTree`

- Element(), SubElement(), tag, text, attrib, dump(), write()

# 궁금한 것

# 레퍼런스

### 유니코드

**[유니코드 테이블](https://ko.wikipedia.org/wiki/%EC%9C%A0%EB%8B%88%EC%BD%94%EB%93%9C_%EC%98%81%EC%97%AD)[유니코드와 UTF-8](https://medium.com/@jeongdowon/unicode%EC%99%80-utf-8-%EA%B0%84%EB%8B%A8%ED%9E%88-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-b6aa3f7edf96)[UTF-8과 UTF-16](https://pickykang.tistory.com/13)**

# Day 04

# 알게된 것

- 디폴트 매개변수는 항상 뒤쪽에 와야함
- 슬라이싱은 `start:end-1:step`
- 메모이제이션

# 질문

- 연산자 우선순위
- while문의 조건이 시간에 따라 어떻게 변하는지, 절차대로 수행하는지 아니면 조건문을 충족하지 않은 순간 펑인지
- 파이썬에 NoneType이 왜 필요한지

# Day 03
# 학습 목표 및 목차

### 학습 목표

---

- Git과 GitHub의 차이
    - Git은 버전관리 어플리케이션. Github는 git을 클라우드 환경에서 업로드하는 원격 저장소. 흔히 제일 많이 쓰이고, 다른 거는 gitlab 등이 있음

        → git은 소스코드 버전 관리 시스템

        → github은 버전 관리 호스팅 사이트

- Git의 add, commit, push, pull
    - add : 스테이지 영역으로 올리는 것
    - commit : 스테이지 영역에서 확정하는거 (push와 pull시 commit이 되어있어야함)
    - push : 원격저장소에 깃을 업로드 하는 것
    - pull : 원격저장소에 업로드되어 있는 것을 받아오는 것
- Github 소스코드 버전 관리
    - 일반적인내용일듯
- Jupyter Notebook
- 마크다운 문법

# 사전 궁금증

- add 와 commit 시 각각 stage 영역을 왔다갔다 하는데, 영역을 정확히 모르겠다

# 몰랐던 것

### Git의 Repository 구조

![스크린샷 2021-09-09 오전 10.08.30.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/cd34d7c6-36b2-4283-8afa-c400c3000194/스크린샷_2021-09-09_오전_10.08.30.png)

작업폴더(Working directory), 인덱스(Staging Area), 저장소(Head-Repository)

**작업폴더**

- 우리가 작업하는 폴더

**인덱스**

- commit을 실행하기 전에 작업트리와 저장소 사이에 존제하는 가상의 영역

작업폴더에서 Untracked files(추가), Modified files(변경)을 인덱스에 stage(기록) 해야만 commit 할 수 있음 → git add

`git rm --cached <files>` 를 통해서 인덱스에 추가된 파일 제외 가능

---

# 더 나아가기 (질문)

```python
git add .

git commit -a -m

git commit -am

gcam

다똑같은거 맞나?
```

- 원격저장소에 이미 올라간 파일 삭제하는 매커니즘 이해하기

git push -u 할때 u가 정확히 뭐지

ssh-keygen을 해서 만들면 뭐 문제가 있나 → 없는듯

[Git - SSH 공개키 만들기](https://git-scm.com/book/ko/v2/Git-서버-SSH-공개키-만들기)

**단상**

token 방식이 30일짜리 발급받으면 30일동안은 써도 되는 개념이면 그냥 token으로 하는 것도 나쁘지는 않을 것 같다.

- Pandas, Matplotlib, Seaborn 이용 그래프 그리기
- 시각화를 해보고 EDA를 하며 인사이트 도출
# 몰랐던 것

### `%matplotlib inline`

IPython에서 사용하는 매직메서드. notebook을 실행한 브라우저에서 바로 그림을 볼 수 있게 해줌.

[ipython 의 매직명령어들](https://studymake.tistory.com/601)

### `plt.plot()`

- plot을 그릴 때는 figure() 객체를 생성하고 add_subplot으로 서브 플롯을 생성해야 함.
- 위 명령으로 그래프를 그리면 matplotlib은 가장 최근의 figure 객체와 서브플롯을 그림. 없으면 서브플롯 하나를 생성

### 범주형 데이터

- 주로 막대 그래프를 사용하여 수치를 요약
- 일반적으로 가로, 세로, 누적, 그룹화된 막대 그래프 사용

### 템플릿

```python
fig = plt.figure() # 새로운 figure 만들어줌
ax1 = add_subplot(1,1,1) or plt.plot(x=,y= ...)
plt.bar or plt.hist or sns.barplot(df, x=, y=) sns.scatterplot etc... #seaborn은 바로 df를 매개변수로 넣어줌
```

# 궁금한 것

```python
>>>

Text(0.5, 1.0, "Yuna's Test Result")
```

시각화를 하고 나오는 값 (0.5, 1.0)의 뜻

### plot 그리기

- plt.show()를 하면 아직 안 넣은 기존에 값이 나오거나 값이 제대로 나오지 않음 어떻게 처리?
- 다 그렸다가 처음부터 다시 그릴때 주의사항

- 한번에 하면 실행이 되고, 쉘을 나눠서 작업하면 plt따로fig따로 그려짐
