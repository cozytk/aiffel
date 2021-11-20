
### 목표

- 데이터를 연산하는 방법 학습
- Pandas, Class를 이용한 데이터 연산법 연습
- Database에 대해 학습, Python을 이용해 간단한 Database 직접 사용

### 내용

1. 데이터 관리 프로그램 만들기
    - 파일 시스템 활용
    - 판다스와 csv 파일
    - 판단스의 유용한 기능
    - 판다스 Transform 실전연습
2. 데이터베이스
    - 다중 사용자 환경
    - 데이터베이스의 세계로
    - SQL
    - 파이썬 DB API
    

### SQL

- 쿼리(query)를 위한 언어
- Pandas를 이용하면 SQL과 유사한 기능을 수행할 수 있음

### pandas 합치기 메소드

### `pd.merge(df1, df2, on=, how=inner(d)|outer`

- 두 데이터프레임 간 공통의 칼럼을 키로 사용해 데이터를 합쳐줌
- on 인자로 공통으로 사용할 칼럼을 지정. 공통된 칼럼이 하나인 경우 자동으로 해줌
- how 인자로 공통의 데이터만 합치는 inner join, 모두 합치고 NaN으로 처리하는 outer join을 할 수 있음

### `df1.join(df2, how='outer', lsuffix='_caller', rsuffix='_other')`

- '_caller'인 df1 컬럼이 왼쪽에 가도록 배치

### `pd.concat([df1,df2], sort=, ignore_index=)`

- 이어 붙이기. 적층 또는 연결

### SQL Join Chart

[SQL Join Chart - Custom Poster Size](https://www.reddit.com/r/SQL/comments/aysflk/sql_join_chart_custom_poster_size/)

## 데이터베이스

---

### Transaction(트랜잭션)

**정의**

- 데이터베이스의 상태를 변환시키는 하나의 논리적 기능을 수행하기 위한 작업의 단위
- 한꺼번에 모두 수행되어야할 일련의 연산들의 의미

**특징**

1. 데이터베이스 시스템에서 병행 제어 및 회복 작업 시 처리되는 작업의 논리적 단위
2. 사용자가 시스템에 대한 서비스 요구 시 시스템이 응답하기 위한 상태변환 과정의 작업단위
3. 하나의 트랜잭션은 Commite 되거나 Rollback

**성질**

Atomicity, Consistency, Isolation, Durability

**연산**

Commit, Rollback

**상태**

Active, Failed, Aborted, Partially Committed, Committed

[[DB기초] 트랜잭션이란 무엇인가?](https://coding-factory.tistory.com/226)

### DBMS

- 다수 사용자에 대응할 수 있는 데이터 관리 프로세스
- 실시간 트랜잭션 처리 기능을 갖춤
- 데이터의 정합성을 보장

### 데이터베이스, 서버, 데이터만 관리하는 컴퓨터

- 데이터를 만들고, 읽고, 쓰는 작업을 여러 명이 모두 하나의 컴퓨터에 하는 건 매우 힘든 일
- 데이터만을 저장하는 공간을 하나 만듦. 물리적 컴퓨터에 방점을 두어 **데이터 서버 컴퓨터**, 또는 추상적인 정보의 집합에 방점을 두어 **데이터베이스**라고 함
- 데이터만을 위한 데이터 서버 컴퓨터가 있고, 해당 서버에 접근하는 전용프로그램을 이용해서 데이터를 읽고 수정함

**SQL**

- 서버에 있는 데이터베이스의 데이터를 요청하는 Query를 작성하기 위한 언어 중 하나

### 소프트웨어의 요소와 만드는 사람들

- 사용자가 데이터베이스의 데이터를 조회/수정할 수 있도록 인터페이스를 개발자가 제공함

**DBA**

데이터를 어떻게 관리할지, 어떤 항목으로 관리할지 등을 설계하고 데이터베이스에 접근하기 위한 쿼리를 작성

### 관계형 데이터베이스

- 데이터를 column과 row를 이루는 하나 이상의 테이블(또는 관계)로 정리
- Primary Key(고유 키)가 각 로우를 식별

### DDL (데이터 정의어)

- 테이블이나 관계의 구조를 생성
- 테이블, 데이터베이스, 사용자에 대한 생성, 삭제, 제약조건, 권한을 설정
- CREATE, USE, DROP, TRUNCATE

### DML (데이터 조작어)

- 데이터를 조회, 삽입, 갱신, 삭제
- SELECT, INSERT, UPDATE, DELETE

### 파이썬 DB-API

- 파이썬 인터프리터는 데이터베이스를 바로 사용할 수 있도록 표준 API 지원
- MySQL 뿐만 아니라 SQL기반 데이터베이스를 어떤 것이드 사용할 수 있음
- 데이터베이스 전용 드라이버만 설치하고 SQLite는 이미 내장