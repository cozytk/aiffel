# 알게된 것

### 파이썬의 모든 것은 객체

- 클래스가 책임지는 것은 변수 할당과 object id 부여

### 클래스 선언

```python
Class A:
	pass

Class A():
	pass
```

- 클래스 이름 다음 소괄호는 선택

### 표기

```python
# 클래스
mycar -> MyCar
# 함수
mycar -> my_car
```

### 클래스 변수와 인스턴스 변수

```python
Class A:
	attr1 = "something"

	def __init__(self):
		attr2 = "something"
```

- attr1을 클래스 변수,  attr2를 인스턴스 변수라고 부름

### 추상화와 캡슐화

**추상화(abstraction)**

복잡한 자료, 모듈, 시스템 등으로부터 핵심적인 개념 또는 기능을 간추려 내는 것

**캡슐화(encapsulation)**

객체의 속성과 행위(메소드)를 하나로 묶는다.

실제 구현 내용 일부를 외부에 감추어 은닉한다.

### 메소드 오버라이드

- 부모 객체에 있는 메소드를 자식 객체에서 다시 선언하는 것.

# 궁금한 것

```python
var = [1,2,3]
a = var
```

위와 같은 경우를 파이썬에서 얕은 복사라고 볼 수 있을까?