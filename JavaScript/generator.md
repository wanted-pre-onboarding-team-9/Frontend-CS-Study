# Generator에 대해 설명해주세요.

1. **Generator Function**

   generator를 반환합니다.

   `function* generatorFunction() { /* ... */ }`와 같이 사용합니다.

   한 번의 실행으로 함수의 끝까지 실행이 완료되는 일반 함수와는 달리 `yield`와 `next`를 통해 일시적으로 정지될 수도 있고, 다시 시작될 수도 있습니다.

2. **Generator**

   제너레이터 함수의 반환으로 iterable 프로토콜과 iterator 프로토콜을 따르는 객체입니다. 제네레이터의 이터러블에서 반환하는 이터레이터는 자기 자신입니다.

   ```jsx
   function* generatorFunction() {
     yield 1;
   }

   const generator = generatorFunction();

   generator === generator[Symbol.iterator]();
   ```

3. **yeild / next**

   `yield`는 제너레이터 함수의 실행을 일시적으로 정지시키며, `yield` 뒤에 오는 표현식은 제너레이터의 caller에게 반환됩니다. (일반 함수의 `return`과 유사)

   여기서 제너레이터 함수는 Callee이고, 이를 호출하는 함수가 Caller이며, Caller는 Callee의 `yield`부분에서 다음 statement로 진행을 할 지 여부를 제어합니다. 이는 `next`로 인해 재개될 수 있습니다.

   ```jsx
   function* sayHiGenerator(params) {
     yield "hello";
     yield "world";
     // statements
     return "hi";
   }

   const resultGenerator = sayHiGenerator();
   console.log(resultGenerator); // { [Iterator] } -> generator object
   ```

   ```jsx
   console.log(resultGenerator.next()); // { value: 'hello', done: false } -> still in suspender state
   console.log(resultGenerator.next()); // { value: 'world', done: false } -> still in suspender state
   console.log(resultGenerator.next()); // { value: 'hi', done: true } -> finished
   console.log(resultGenerator.next()); // { value: undefined, done: true } -> nothing to return here
   ```

   next가 리턴하는 객체에서 `value`는 yield expression이 반환할 값(즉, yielded value)이고, `done`은 Generator 함수가 가장 마지막 값을 `yield`했는지 여부를 boolean 값으로 나타낸 것을 의미합니다.

## References

[Iterators and generators - JavaScript | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Iterators_and_Generators) <br />

[[Js] 자바스크립트, Generator 함수에 대하여](https://im-developer.tistory.com/193)
