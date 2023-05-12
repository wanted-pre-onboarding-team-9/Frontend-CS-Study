# Blocking과 Non-Blocking, Sync와 Async는 어떤 차이가 있나요?

- Blocking과 Non-Blocking, Sync와 Async의 차이는 작업의 수행방식을 바라보는 관점의 차이에 있습니다. blocking과 non-blocking은 제어권, Sync와 Async는 순서와 결과(처리)를 기준으로 구분됩니다.
- blocking과 non-blocking은 호출되는 함수의 처리가 끝나기 전에 리턴해주는가 아닌가(다른 주체가 작업할 때 자신의 제어권이 있는지 없는지)에 달려있습니다. 호출된 함수가 바로 리턴해서 호출한 함수에게 제어권을 넘겨주고, 호출한 함수가 다른 일을 할 수 있는 기회를 줄 수 있으면 non-blocking, 호출된 함수가 자신의 작업을 모두 마칠 때까지 호출한 함수에게 제어권을 넘겨주지 않고 대기하게 만든다면 blocking입니다.
- sync와 async의 차이는 호출되는 함수의 작업 완료 여부를 누가 신경쓰느냐, 다른 작업의 결과를 바로 처리하느냐에 달려있습니다. synchonous란 호출되는 함수의 작업 완료를 호출한 함수가 신경 쓰는것입니다. 같은 흐름에서 작업을 순차적으로 실행하기 때문에 순서가 보장됩니다. asynchonous란 호출되는 함수의 작업 완료를 호출된 함수가 신경쓰는 것입니다. 비동기 작업에서는 특정 작업의 완료 여부와 상관없이 다음 작업을 수행하기 때문에 작업들의 시작, 종료가 일치하지 않으며 끝나는 동시에 시작을 하지 않음을 의미합니다.
  [![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcjbtU6%2FbtrLuwNTu8L%2FV8EJ8wqKeXDKkx4YyPW4k1%2Fimg.png)
  ](https://velog.io/@tess/Sync-Async-vs-Blocking-non-Blocking)

## References

https://inpa.tistory.com/entry/👩%E2%80%8D💻-동기비동기-블로킹논블로킹-개념-정리# <br/>
https://velog.io/@tess/Sync-Async-vs-Blocking-non-Blocking
