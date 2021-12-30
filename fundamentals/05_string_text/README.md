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