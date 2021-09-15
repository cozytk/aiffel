# Day 02
# 학습목표

- 운영체제의 구성과 커널의 역할
    - 운영체제는 커널과 기타 이것저것으로 구성되어 있음
    - 커널은 스케쥴링을 담당

        → 보안, 자원관리, 디바이스 인터페이스 추상화 등

- 터미널과 터미널 에뮬레이터, 셸의 차이점
    - 터미널은 CLI 인터페이스

        → 컴퓨터에 정보를 입력하고 출력하는 소프트웨어 및 하드웨어로써의 장치

    - 터미널 에뮬레이터 ?
        - 그래픽 환경에서 터미널을 묘사
    - 셸 터미널 내부에서 터미널의 제어 접근을 도와주는 프로그램
- 기본적인 리눅스 명령어
    - 기본은 많이 아는듯

# 몰랐던 것

### 프롬포트 의미

![스크린샷 2021-09-08 오전 10.00.00.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e9eb5107-1bfd-4ddc-ae27-3334555786e9/스크린샷_2021-09-08_오전_10.00.00.png)

- #(현재 로그인한 사용자가 최고 관리자 계정), 일반 사용자의 경우 $

### help 페이지 위 아래로

`shift + PgUp | PgDown`

- **일부 주요 폴더들의 용도 및 내용물**

    **`/home`: 사용자별 홈 디렉토리들이 있는 곳**

    **`/root`: 최고 관리자 계정의 홈 디렉토리**

    **`/mnt`: 저장장치(HDD, SSD)가 붙는 위치**

    **`/media`: 이동식 미디어(USB 드라이브)가 붙는 위치**

    **`/tmp`: 재부팅 시 삭제될 임시 파일들을 저장하는 폴더**

    **`/dev`: 컴퓨터에 연결된 하드웨어 및 가상 기기(device)들을 가리키는 파일들**

    **`/proc`: 현재 실행 중인 프로세스들을 가리키는 파일들**

    **`/etc`: 각종 설정 파일들**

    **`/bin`: 실행 가능한 프로그램(binary)들**

    **`/sbin`: 시스템 관리용 프로그램들**

    **`/usr`: 다중 사용자 모드에서 사용 가능한 파일 및 프로그램들 (root 계정만 있는 단일 사용자 모드에서는 사용 불가)**

    **`/var`: 캐시, 로그 등 시스템 구동 간 계속 내용이 바뀌는 파일들**

### 운영체제별 커널

우분투 → 리눅스

윈도우 → Windows NT

macOS → XNU

### 프로세스 격리

- 운영체제는 프로세스 컴퓨터의 전체 메모리 어디든지 쓸 수 있도록 하는 것이 아니라 **가상 메모리**로써 일부만 떼어서 제공해줌
- 다른 프로세스의 메모리 또는 운영체제 자체가 사용하고 있는 **커널 메모리**를 훔쳐볼 수 없도록 함
- 프로세스들이 서로 소통하기 위해서는 별도로 허용된 프로세스 간 통신 (IPC) 기법들을 사용해야함
    - IPC 기법 : PIPE,  Named PIPE(FIFO), Meesage Queue, Shared Memory(공유 메모리), Memory Map, Socket

### CPU 자원 관리

- CPU 연산의 경우 **코어 단위**로 프로세스에 제공
- 프로세스는 **스레드**라는 단위로 코어를 하나씩 사용
- 프로세스가 하나 시작되면 기본적으로 하나의 스레드를 가지고 시작하지만, 개발자는 프로그램이 더 많은 스레드를 사용하도록 설계하여 다중 CPU 코어의 이점 극대화
- 프로세스는 운영체제가 메모리를 할당하는 **작업단위,** 스레드는 프로세스가 할당받은 메모리를 활용하는 **실행단위**

### ps

![스크린샷 2021-09-08 오전 10.48.41.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0b140580-f3af-4c71-8bfd-562f2689f970/스크린샷_2021-09-08_오전_10.48.41.png)

`UID`: User ID, 프로세스마다 누구의 권한으로 실행되는가

`TTY`: 프로세스(PID)가 붙어있는 teletype(터미널)

`pts/n` : n번 가상터미널(pseudo teletype slave)

`?`: 터미널에 부착되지 않은 프로세스들

### 시스템 콜

- 프로세스가 커널에게 요청을 전달하는 기능
- 커널이 프로그램에 제공하는 인터페이스
- 각 프로세스는 커널을 통하지 않고서는 파일이나 장치, 또는 다른 프로세스에 간섭할 수 없음

`kill`: 그 자체로 프로세스를 죽이는 명령어이 아니라, 프로세스에 신호를 보내는 명령어

- KILL 신호말고 INT(interrupt, ctrl+c), TERM(terminate) 신호도 있음

### 환경 변수

운영체제가 프로세스 단위로 사용하는 변수

### $PATH 의 :

동일한 이름의 프로그램이 여러 디렉토리에 설치되어 있으면, `PATH` 내 순서 상 앞에 있는 디렉토리의 프로그램을 실행

### 패키지 관리자

- APT(Advanced Packaging Tool)
- 운영체제가 공식적으로 제공
- 공인 저장소에서 프로그램과 라이브러리(다른 프로그램이 참조하여 사용할 수 있는 코드)
- 운영체제상: 우분투 apt,snap Centos YUM, Red Hat rpm 등등
- 프로그래밍 언어상: 파이썬 pip

### 한 컴퓨터 여러 사용자

개인용 컴퓨터 시대의 운영체제에도 그대로 남아있음.

특히, 유닉스 계열 운영체제들은 개인용 컴퓨터보다 서버용 또는 기타 산업용으로 쓰이는 경우가 잦기에, 다른 운영체제보다 사용자와 권한의 개념을 훨씬 더 자주 마주치게 됨

### 사용자 계정

보통 우리가 사용하는 사용자 계정은 운영체제를 설치할 때 최초로 생성한 계정

최고 관리자: 윈도우-Administrator, 유닉스계열-root

### 사용자 그룹

사용자들이 여러 명 있을 떄, 쉽게 묶어서 관리하는 개념

한 사용자가 `sudo` 명령어를 실행하기 위해서는, 동일한 이름 `sudo` 라는 이름의 그룹에 속해있어야함

### 현재와 상위 디렉토리

![스크린샷 2021-09-08 오전 11.39.27.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d6679dd9-242f-4d15-8229-bd07a4af634e/스크린샷_2021-09-08_오전_11.39.27.png)

- 실제 현재 디렉토리와 상위 디렉토리 나타내는 거였음

### chown

그냥 사용하면 디렉토리의 소유자가 변경되고 `-R` 을 사용하면 디렉토리 내의 모든 파일들에 대한 소유자가 변경됨

### 디렉토리 권한

실행하기(x)의 경우 프로그램이라면 실제 실행할 수 있다는 것을 나타내지만, **디렉토리의 경우 해당 폴더 안으로 cd로 이동할 수 있는지** 여부

### ARM

스마트폰 등 모바일 기기에 들어가는 CPU ARM사의 RIS

지원하는 명령어는 더 적지만 전력을 더 적게 소비하는 방향으로 설계

더 이상 칩을 만들지 않고, 설계만 만들어 라이센스를 판매

삼성전자(엑시노스), 애플(A11), 퀄컴(스냅드래곤) 등

### 클럭

초당 처리 속도 기준

요즘 나오는 CPU는 클럭이 4GHz에서 더 이상 발전하기 보다 동시에 더 많은 스레드를 처리할 수 있도록 코어를 늘리는 방향으로 제조

### GPU

 - 그래픽 연산장치

- CPU 보다 이해할 수 있는 명령어는 훨씬 적지만, 코어 수를 훨씬 늘리는 방법으로 다차원 행렬에 특화

### 기타 연산장치

- ASIC (작업에 맞게 직접 설계), FPGA(그때그떄 회로를 직접 프로그래밍해서 사용)

### 딥러닝과 저장장치

- GPU를 쓰면 '연산'이 빨라져 딥러닝 모델이 무조건 빨라질 것 같지만 아님
- 데이터를 읽어오는 데 시간이 너무 많이 소요되고 있다면
    - 저장장치 SSD로 변경
    - 미리 여러 개의 스레드를 사용하여 RAM 메모리에 올려둠

### 가상화

아마존 - 한대의 물리적인 서버를 여러 개의 가상 서버로 쪼개어 판매

물리적인 서버를 임대하는 것이 아님

하나의 컴퓨터를 쪼개어 여러 대의 컴퓨터가 있는 것처럼 사용하게 하는 기술

호스트: 실제 물리적인 서버, 게스트: 그안에서 돌아가는 가상 서버

**종류**

가상머신 가상화: 게스트 자체에 운영체제가 돌아감

컨테이너 가상화: 호스트의 운영체제 커널을 공유 (커널의 기능만 공유하고, 프로세스나 자원 철저히
                                                                           격리하며 간섭 X)

- 가상화가 무조건 클라우드 컴퓨팅과 함께하는 개념은 아님
    - 아나콘다나 virtualenv는 클라우드 컴퓨팅과 크게 관계가 없지만 가상화의 한 종류

### 편리한 기능

**터미널 에뮬레이터에서 무언가를 복사하거나 붙여넣을 때에는 `Ctrl+Shift+C`, `Ctrl+Shift+V`를 사용해야 합니다.**

**`history` 명령에서 나오는 번호를 참고하여 `!번호`를 실행하면 해당 번호의 명령이 다시 실행됩니다.**

**`Ctrl+A`, `Ctrl+E`를 통해 명령어의 앞, 뒤로 커서를 이동할 수 있습니다.**

**`clear` 명령어 또는 `Ctrl+L`을 통해 기존에 터미널에 출력되었던 내용을 깨끗이 지울 수 있습니다.**

**실수로 `Ctrl+z`를 눌러 프로세스를 중지시켰다면, `fg`를 통해 다시 재개시킬 수 있습니다.**

**`sudo apt install curl` 및 `curl parrot.live`를 통해 춤추는 앵무새를 볼 수 있습니다.( 클라우드에서는 작동이 안되니 로컬에서 테스트 해보세요 !)**

### 심화 명령어

[Aiffel](https://lms.aiffel.io/steps2/133)

---

# 질문

**2-8**

코어 수마다 실행할 수 있는 프로세스와 쓰레드의 개수가 정해져있지 않을까?

- CPU가 n코어 m스레드라고 말하는데, n코어개만큼의 프로세스만 물리적으로 병렬적 실행이 가능한거고 (스케줄링)없이 동시에 실행 가능한 스레드의 개수가 프로세스 개수만큼인데 요즘은 프로세스별로 하나 이상의 스레드를 지원하시도함

**2-9**

- 터미널의 번호가 여러개 있고 프로세스에 붙어있다는 개념

**2-10**

![스크린샷 2021-09-08 오전 10.53.53.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7becfe30-d5a4-4044-9683-c405ae6378cf/스크린샷_2021-09-08_오전_10.53.53.png)

**2-11**

환경 변수를 운영체제가 프로세스 단위로 사용하나?

→ 탭을 여러개 켜놓고 실행해보니 맞음

![스크린샷 2021-09-08 오전 11.02.18.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/9d76958b-b0eb-4c11-a67c-615d68e5fc2b/스크린샷_2021-09-08_오전_11.02.18.png)

- zsh를 탭단위로 열때마다 CMD가 4개씩 생김 (왜지)

![스크린샷 2021-09-08 오전 11.10.09.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b6f37dad-6a0f-41e3-aa8a-366c8122198d/스크린샷_2021-09-08_오전_11.10.09.png)

- export가 현재 환경으로 내보낸다, 그리고 env가 새로운 환경에서 실행한다는 무슨 의미일까?

**2-13**

- 모든 것들은 파일로 저장이 되어있는데 내 현재 위치가 어디인지 저장되어있는 파일은 어디에 이쓸까

**2-18**

셸에도 파이썬처럼 조건문과 연산자들이 있습니다. ||를 써서 이전 명령이 false를 반환한 경우에만 다음 명령을 실행하거나, &&로 이전 명령이 true를 반환한 경우에만 다음 명령을 실행할 수 있습니다.

→ 실험해봄 실제로 그럼


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

# Day 04

# 알게된 것

- 디폴트 매개변수는 항상 뒤쪽에 와야함
- 슬라이싱은 `start:end-1:step`
- 메모이제이션

# 질문

- 연산자 우선순위
- while문의 조건이 시간에 따라 어떻게 변하는지, 절차대로 수행하는지 아니면 조건문을 충족하지 않은 순간 펑인지
- 파이썬에 NoneType이 왜 필요한지

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