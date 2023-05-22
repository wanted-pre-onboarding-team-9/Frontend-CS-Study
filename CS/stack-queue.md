# 스택과 큐 자료구조에 대해 설명해주세요.

## 자료구조
- 자료(데이터)에 효율적으로 접근, 수정하기 위하여 자료를 조직하고 관리하고 저장하는 방법을 의미
- 왜 필요한가?
  - 상황에 따라 데이터를 다루는데 시간, 메모리를 효율적으로 사용해야 하기 때문
- 형태에 따라 크게 2가지로 나뉨
  - 선형 자료구조
  - 비선형 자료구조

## 1. 선형 자료구조
- 자료를 구성하는 데이터들이 직선 형태로 순차적 나열되어 있는 구조
- 전후 데이터들 간 일대일(1:1) 관계
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F99E5544F5C80F3631F)

## 2. 비선형 자료구조
- 하나의 자료 뒤에 여러개의 자료가 존재할 수 있는 구조
- 전후 데이터들 간 일대다(1:N)의 관계
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F99B2A74E5C80F3EA18)

## 자료구조의 종류 도식화
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F9912A0355C80DFAD02)


---

## 스택과 큐 한눈에 보기
![](https://gohighbrow.com/wp-content/uploads/2018/07/Computer-science-fundamentals_6.1.png)

## 스택(stack)
- 데이터를 쌓아 올리듯이 쌓아서 저장하는 자료구조
- 가장 마지막에 쌓인 데이터가 가장 먼저 나가는 후입선출(LIFO, Last-In-First-Out) 구조
- 함수의 호출과 반환, 수식의 계산, 브라우저의 뒤로가기/앞으로가기 등 다양한 곳에서 사용됨
- 활용 가능한 메서드
  - `push`: 순서대로 데이터를 넣어줌
  - `pop`: 마지막 데이터를 꺼냄
  - `peek`: 스택에 쌓인 데이터의 가장 마지막 데이터를 보여주기'만' 하는 것(데이터가 지워지는 것이 아님)
- 특정 상태
  - stack underflow: 비어있는 스택에서 원소를 추출하려 할 때
  - stack overflow: 스택이 넘치는 경우

## 큐(queue)
- 먼저 들어온 데이터가 먼저 나가는 선입선출(FIFO, First-In-First-Out) 구조
- 대기열이나 작업 처리 등에서 사용됨

## 번외. 덱((Deque)
- 양방향 큐(Double Ended Queue) 라고도 함
- 큐의 처음과 끝에서 모두 삽입과 삭제가 가능한 자료구조

## References

- [인생의 로그캣: [자료구조] 스택, 큐, 데크](https://noahlogs.tistory.com/28)
- [[자료구조] 스택, 큐, 덱](https://cotak.tistory.com/69)
