# [ ****화살표 함수와 일반 함수의 차이**** ]

> **화살표 함수(Arrow Function)는 ES6에서 새로 추가되었고 기존 함수 표현식과 비교하면 간단하게 사용 가능하며 익명 함수로 이름이 없는 함수, 즉시 실행이 필요할 경우 사용하는 함수이다.**

- **일반 함수 사용 방법**

  ```jsx
  function test() {
    console.log("test");
  }
  ```

  ```jsx
  const abc = function test() {
    console.log("test");
  };
  ```

- **화살표 함수 사용 방법**

  ```jsx
  const test = () => {
    console.log("test");
  };
  ```

<br />

- **화살표 함수와 일반 함수의 차이점은?**

  - this 바인딩
  - 생성자 함수로 사용 가능 여부
  - arguments 사용 가능 여부

<br />

1. this 바인딩 ( 자바스크립트에서 모든 함수는 실행될 때마다 함수 내부에 this라는 객체가 추가된다. )

   - 일반 함수
     - 함수 실행 시에는, 전역(window)객체를 가리킨다.
     - 메소드 실행 시에는 메소드를 소유하고 있는 객체를 가리킨다.
     - 생성자 실행 시에는 새롭게 만들어진 객체를 가리킨다.
   - 화살표 함수

     - 선언할 때 this에 바인딩할 객체가 정적으로 결정된다.
     - 언제나 상위 스코프의 this를 가리킨다.
     - 또한, call, apply, bind 메소드를 사용하여 this를 변경할 수 없다.

        <br />

     ```jsx
     function test() {
       this.name = "하이";
         return {
           name: "바이",
             speak: function () {
               console.log(this.name);
             },
         };
     }

     function arrTest() {
       this.name = "하이";
         return {
           name: "바이";
             speak: () => {
               console.log(this.name);
             },
         };
     }

     const test1 = new test();
     test1.speak(); // 바이

     const test2 = new arrTest();
     test2.speak(); // 하이
     ```

     - 일반 함수로 사용했을 때는 ‘바이’가 찍히고 화살표 함수를 사용했을 때는 ‘하이’가 찍힌다.
     - 일반 함수는 자신이 종속된 객체를 this로 가리키고 화살표 함수는 자신이 종속된 인스턴스를 가리킨다.

   <br />

2. 생성자 함수로 사용 가능 여부

   ```jsx
   function test() {
     this.num = 1234;
   }
   const arrTest = () => {
     this.num = 1234;
   };

   const testA = new test();
   console.log(testA.num); // 1234

   const testB = new arrTest(); // Error
   ```

   - 일반 함수는 생성자 함수 사용할 수 있지만 화살표 함수는 prototype 프로퍼티를 가지고 있지 않기 때문에 사용할 수 없다.

      <br />

3. arguments 사용 가능 여부

   ```jsx
   function test() {
     console.log(arguments); // Arguments(3) [[1, 2, 3, callee: ƒ, Symbol(Symbol.iterator): ƒ]
   }

   test(1, 2, 3);
   ```

   ```jsx
   const arrTest = () => {
     console.log(arguments); // Uncaught ReferenceError: arguments is not defined
   };

   arrTest(1, 2, 3);
   ```

   - 일반 함수에서는 한수가 실행될 때 암묵적으로 arguments 변수가 전달되어 사용 가능하지만 화살표 함수에서는 arguments 변수가 전달되지 않는다.
