### 목표

- 멀티태스킹, 병렬프로그래밍과 동시성
- 멀티스레드와 멀티프로세스 구현
- `concurrent.futures` 이용한 병렬프로그래밍 구현

### 목차

1. 멀티태스킹
    - 멀티태스킹이란
    - 컴퓨터의 세계 - 프로그램
    - 프로그램 실행과 프로파일링
    - scale-up vs scale-out
2. 멀티프로세스, 멀티스레드
    - 멀티스레드
    - 멀티프로세스
    - 스레드/프로세스 풀
3. 실전 예제
    - concurrent.futers 모듈
    - 소수 구하기 문제

## 멀티 태스킹

---

### 동시성

하나의 processor가 여러 가지 task를 동시에 수행

### 병렬성

여러 processor가 동시에 수행

※ CPU가 점차 발전되면서 병렬성의 의미가 확장

[Concurrency vs. Parallelism](http://tutorials.jenkov.com/java-concurrency/concurrency-vs-parallelism.html)

### Synchronous(동기)

- 어떤 일이 순차적으로 실행됨.
- 요청과 요청에 대한 응답이 연속적으로 실행
- 요청에 지연이 발생하더라도 계속 **대기**

## Asynchronous(비동기)

- 어떤 일이 비순차적으로 실행됨
- 요청과 요청에 대한 응답이 연속적으로 실행 X
- 특정 코드의 연산이 끝날 때까지 코드의 실행을 멈추지 않고 다음 코드를 먼저 실행
- 중간에 실행되는 코드는 주로 콜백함수로 연결

### I/O Bound

입력과 출력에서의 데이터(파일)처리에 시간이 소요될 때

### CPU Bound

복잡한 수식 계산이나 그래픽 작업과 같은 엄청난 계산이 필요할 때

※ more about bound

[What do the terms "CPU bound" and "I/O bound" mean?](https://stackoverflow.com/questions/868568/what-do-the-terms-cpu-bound-and-i-o-bound-mean)

### Process (프로세스)

- An Instance of a program (ex. Python Interpreter)

### 프로세스 관련 정보 얻기

```python
import os

# process ID
print("process ID:", os.getpid())
# user ID
print("user ID:", os.getuid())
# group ID
print("group ID:", os.getgid())
# 현재 작업중인 디렉토리
print("current Directory:", os.getcwd())

>>>

process ID: 43
user ID: 0
group ID: 0
current Directory: /aiffel
```

```bash
ps -ef | grep 43

>>>

root        43     6  0 07:50 ?        00:00:00 /opt/conda/bin/python -m ipykernel_launcher -f /aiffel/.local/share/jupyter/runtime/kernel-89de6bf0-e975-4a00-8c21-b72acaca7957.json
root        89    85  0 07:59 pts/0    00:00:00 grep 43
```

- pid 43은 aiffel LMS가 연결한 jupyter 커널 프로세스였음

### 스레드

- 어떠한 프로그램 내, 특히 프로세스 내에서 실행되는 흐름이 단위
- 프로세스는 자신만의 전용 메모리 공간(Heap)을 가짐. 이때 해당 프로세스내의 스레드들은 이 메모리 공간을 공유하지만 다른 프로세스와 공유하지는 않음

### 프로파일링

- 코드에서 시스템의 어느 부분이 느린지 혹은 어디서 RAM을 많이 사용하고 있는지를 확인하고 싶을 때 사용하는 기법
- 애플리케이션에서 가장 자원이 집중되는 지점을 정밀하게 찾아냄

  **프로파일러**

- 애플리케이션을 실행시키고 각각의 함수 실행에 드는 시간을 찾아내는 프로그램
- 코드의 bottleneck(병목)을 찾아내고 성능을 측정해주는 도구

  **프로파일링 도구**

- cProfile, line_profiler

**[파이썬 프로파일러 - cProfile, profile](https://docs.python.org/ko/3/library/profile.html)**

**[line profiler를 사용하여 파이썬의 각 라인이 어떻게 돌아가는지를 알아보자.](https://frhyme.github.io/python-libs/python_line_profileing_in_python/)**

### Scale_ Up

- 한 대의 컴퓨터의 성능을 최적화시키는 방법

### Scale Out

- 여러 컴퓨터를 한 대처럼 사용하는 것