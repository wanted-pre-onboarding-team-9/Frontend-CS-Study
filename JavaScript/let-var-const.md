# [ let, var, const ]

<br />

> **`var`, `let`, `const`는 모두 자바스크립트에서 변수를 선언할 때 사용하는 키워드이며 각 키워드는 변수의 범위와 재선언 및 재할당 가능 여부 등에 차이가 있습니다.**

<br />

- **재할당 및 중복 선언**

1. **var : 중복 선언 및 재할당 가능**

   ```jsx
   var test = 1;
   console.log(test); // 1

   var test = 2;
   console.log(test); // 2

   test = 3;
   console.log(test); // 3
   ```

   자바스크립에서는 변수를 먼저 선언 후 값을 할당하는 게 정상적입니다.

   하지만 var의 경우 선언 전에 값을 미리 할당할 수 있으며 출력까지도 해볼 수 있습니다.

   위 코드와 같이 이미 선언한 변수를 동일한 이름으로 재선언(중복 선언) 할 수 있으며 값을 재할당하는 것 또한 가능합니다.

   그리고 마지막에 할당된 값이 최종 변수에 저장됩니다.

   추가적으로 var의 경우 변수를 유연하게 사용할 수 있지만, 기존에 선언해둔 변수의 존재를 잊고 재선언 하는 경우 문제 발생 여지가 있을 수 있습니다. 또한, 간단한 코드가 아닌 길고 복잡한 코드에서 같은 이름의 변수가 여러번 선언되어 사용된다면 어떤 부분에서 값이 변경되고 문제가 발생하는지 파악하기 힘든 단점이 있습니다.

<br />

2. **let : 중복선언 불가, 재할당 가능**

   ```jsx
   let test = 1;
   console.log(test); // 1

   let test = 2;
   console.log(test);
   //Uncaught SyntaxError: Identifier 'title' has already been declared

   test = 3;
   console.log(test); // 3
   ```

   let은 var와 달리 중복 선언 시, 해당 변수는 이미 선언되었다는  `SyntaxError`를 발생시킵니다.
   즉, 중복 선언이 불가합니다. 하지만 변수에 값을 재할당하는 것은 가능합니다.

<br />

3. \***\*const : 중복 선언 및 재할당 불가\*\***

   ```jsx
   const test = 1;
   console.log(test); // 1

   const test = 2;
   console.log(test);
   //Uncaught SyntaxError: Identifier 'title' has already been declared

   test = 3;
   console.log(test);
   //Uncaught TypeError: Assignment to constant variable
   ```

   let와 const의 차이는 재할당 가능 여부입니다.

   재할당이 가능한 let과 달리 const의 경우 재할당 및 중복 선언이 불가합니다.

   그리고 const의 경우 let과 var와 달리 선언을 했을 때 할당도 같이 해주어야 합니다. 그렇지 않으면 `SyntaxError`를 발생시킵니다.

<br />

- **스코프 ( 유효한 참조 범위가 다릅니다. )**

1. **함수레벨 스코프 (Function Level Scope) : var**

   ```jsx
   function functionLevelScope() {
     if (true) {
       var test = 123;
       console.log(test); //123
     }
     console.log(test);
   }

   functionLevelScope(); //123
   console.log(test); //ReferenceError: a is not defined
   ```

   함수내에서 선언된 변수는 함수 내에서만 유효하고, 함수 내에서는 블록 내외부에 관계없이 유효합니다. 그리고 함수 외부에서는 참조가 불가합니다.

<br />

2. **블록레벨 스코프 (Block Level Scope) : let, const**

   ```jsx
   function blockLevelScope() {
     if (true) {
       let test = 123;
       console.log(test); //123
     }

     console.log(test); // ReferenceError: a is not defined.
   }

   console.log(test); // ReferenceError: a is not defined.
   ```

   함수, if절 외 for, while, try/catch 등 모든 코드블록 ({..}) 내부에서 선언된 변수는 코드 블록 내부에서만 유효합니다.

   그리고 블록 외부에서 부터는 참조가 불가합니다.

<br />

> 결과적으로 **재할당이 필요없는 상수와 객체에는 기본적으로 const**를 사용하는 것이 좋습니다. 의도치 않은 재할당을 방지해주기 때문이 안전하며, 재할당이 필요한 경우 한정적으로 let을 사용하는 것이 좋습니다. 단! 이때 변수의 스코프는 최대한 좁게 만드는 것이 좋습니다.
