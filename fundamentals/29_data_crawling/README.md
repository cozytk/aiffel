### 목표

- 웹에서 데이터에 접근하고 그 데이터를 가져오는 방법
- 웹의 구조와 통신에 대한 기초 지식
- 웹 크롤링용 파이썬 라이브러리에 대해 학습하고 간단한 예제 풀어보기

### 유선 통신

- 옛날에, 그리고 아직까지 데스크탑은 LAN선으로 연결
- 외국까지의 연결은 해저 광케이블로 연결
- `DataLink` (LAN카드)를 거쳐 물리적인 네트워크 영역을 통해 데이터 팻킹르 주고 받음

### 무선 통신

- 프로토콜 규약에 맞게 요청하거나 응답을 하면 2개의 컴퓨터에서 전송/응용 계층에서 원격으로 데이터 교환 가능 (Data link와 Network 계층 없이)
- Network와 Transport를 구성하는 `TCP-IP`  가 가능하게 해줌

### 소켓

*인터넷 연결용 포트*

- 컴퓨터 네트워킹에서 인터넷 소켓, 혹은 네트워크 소켓은 끝점(Endpoint)를 의미함
- 소켓과 소켓 사이의 peer-to-peer 연결을 구현하는 프로토콜이 바로 TCP
- 소켓에는 포트(port) 번호가 붙어있음

### TCP/IP

### **TCP**

Transmission Control Protocol. **소켓 포트** 단위의 송수신 프로토콜

- 포트번호 단위 통신이므로 프로크램 레벨 통신 프로토콜

### **IP**

Internet Protocol. 컴퓨터마다 주어지는 **IP 주소** 단위의 송수신 프로토콜

- IP주소 단위 통신이므로 컴퓨터 레벨 프로토콜

- IP 덕분에 특정 컴퓨터까지는 전달되었지만, 포트번호를 따라 정확하게 소켓까지 전달해 주는 것은 TCP의 역할

※ UDP

- TCP는 두 소켓 간의 쌍방향 독점적 통신이므로 connection 기반의 통신 프로토콜인 반면, UDP는 connection 개념이 없는 비연결형
- 데이터그램을 일방적으로 전송하기 때문에 전송속도는 TCP보다 빠름
- 음성, 영상 데이터 전송에 유리

### TCP/IP Application 프로토콜

- 

---

# 궁금한 점

- UTF-8로 인코딩, UTF-8에서 디코딩하는 과정이 왜 필요하지?

# Reference

크롤링과 아키텍처 - [https://velog.io/@mowinckel/%EC%9B%B9-%ED%81%AC%EB%A1%A4%EB%A7%81%EA%B3%BC-%EC%95%84%ED%82%A4%ED%85%8D%EC%B3%90](https://velog.io/@mowinckel/%EC%9B%B9-%ED%81%AC%EB%A1%A4%EB%A7%81%EA%B3%BC-%EC%95%84%ED%82%A4%ED%85%8D%EC%B3%90) 

크롤링 ? : [https://velog.io/@mowinckel/%EC%9B%B9-%ED%81%AC%EB%A1%A4%EB%A7%81-I](https://velog.io/@mowinckel/%EC%9B%B9-%ED%81%AC%EB%A1%A4%EB%A7%81-I) API SDK' sdk - [https://doozi0316.tistory.com/entry/SDK-API%EC%9D%98-%EA%B0%9C%EB%85%90%EA%B3%BC-%EC%B0%A8%EC%9D%B4%EC%A0%90](https://doozi0316.tistory.com/entry/SDK-API%EC%9D%98-%EA%B0%9C%EB%85%90%EA%B3%BC-%EC%B0%A8%EC%9D%B4%EC%A0%90) 

API란? - [https://steemit.com/kr/@yahweh87/it-api](https://steemit.com/kr/@yahweh87/it-api)