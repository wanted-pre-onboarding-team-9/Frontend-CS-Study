# Promise와 async/await은 무엇이고 차이는 뭔가요?

- `Promise`와 `async/await`는 모두 자바스크립트에서 비동기 처리를 다룰 수 있는 방법입니다.
- `promise`는 내용은 실행되었지만 결과를 아직 반환하지 않은 객체로, Pending (대기)/Fulfilled (이행)/Rejected (실패) 3가지 상태를 가지고 있습니다. 비동기 처리가 완료되지 않았다면 pending, 완료되었다면 fulfilled, 실패하거나 오류가 발생했다면 rejected 상태를 갖습니다. .then()과 .catch()문의 체이닝을 통해 비동기 로직의 성공 여부에 따른 분기 처리가 가능한데, resolve한 반환 값에 대해서는 then()을 통해 결과 값을 반환받을 수 있고, reject 의 반환 값에 대해서는 catch() 를 통해 반환받을 수 있습니다.
- `async/await`는 callback과 Promise의 콜백 지옥, then()지옥이라는 단점을 해소할 수 있으며, async 함수 안에서 await를 통해 promise의 반환 값을 받아올 수 있습니다. 따라서 async/await는 비동기 코드가 동기 코드처럼 읽히게 해주며, 코드가 길어질수록 코드 가독성을 좋게 해줍니다. promise와의 차이점으로 Promise는 .catch()문을 통해 에러 핸들링이 가능하지만 async/await는 에러 핸들링 기능이 따로 없어 try-catch문을 활용해야 한다는 점이 있습니다.

## 참고: 콜백 지옥, then 지옥

**콜백 지옥(callback hell)** 은 비동기 작업을 처리하기 위해 콜백 함수를 중첩하여 사용하는 코드 구조를 말합니다.
콜백 함수를 계속해서 중첩하면서 들여쓰기 수준이 증가하고 코드의 가독성과 유지보수성이 저하됩니다.

```javascript
asyncFunc1(function (result1) {
  asyncFunc2(result1, function (result2) {
    asyncFunc3(result2, function (result3) {
      // ...
    });
  });
});
```

**then 지옥(then hell)** 은 Promise를 사용하여 비동기 작업을 처리할 때 then 메서드를 연속적으로 호출하여 처리하는 코드 구조를 말합니다.
비동기 작업이 연속적으로 이어지면서 then 메서드가 중첩되면 코드의 가독성이 저하되고 복잡성이 증가합니다.

```javascript
asyncFunc1()
  .then(function (result1) {
    return asyncFunc2(result1);
  })
  .then(function (result2) {
    return asyncFunc3(result2);
  })
  .then(function (result3) {
    // ...
  });
```

## References

https://ko.javascript.info/promise-basics <br />
https://ko.javascript.info/async-await <br />
https://springfall.cc/post/7 <br />
