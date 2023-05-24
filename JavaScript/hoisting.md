## [ 호이스팅 ]

<br />

> 사전적 정의 : 끌어올리기

<br />

- **호이스팅 이란?**
  자바스크립트에서 코드를 실행하기 전에 변수와 함수 선언을 메모리에 미리 할당하는 과정입니다.

<br />

우선, 호이스팅에 대해 더 자세히 설명하기 전에 먼저 자바스크립트에서의 변수 처리 과정에 대해 알아보도록 하겠습니다.

- **자바스크립트에서는 총 3단계에 결처 변수를 생성**
  1. 선언 단계 : 변수를 생성하고 등록
  2. 초기화 단계 : 변수는 undefined로 초기화
  3. 할당 단계 : undefined로 초기화된 변수에 실제 값을 할당

<br />
  
| var   | 1. 선언 및 초기화 단계 동시 진행 2. 할당 단계 |
| :---------: | :------: |
| let   | 1. 선언 단계 2. 초기화 단계 3. 할당 단계 |
| const | 1. 선언 + 초기화 + 할당 단계 동시 진행 |

<br />

자, 변수 처리 과정에 대해서 알아보았다면 이제 본격적으로 호이스팅에 대해 조금 더 자세히 알아보도록 하겠습니다.

<br />

> 코드 실행 전 변수와 함수를 메모리에 저장하기 때문에 변수나 함수 선언이 코드 내 어디에 있더라도, 실제 실행 전에 메모리에 할당되어 사용자가 아무 문제 없이 해당 변수나 함수를 사용할 수 있게 됩니다.

<br />

- **호이스팅 동작 방식**
  1. 자바스크립트 parser가 함수 실행 전 해당 함수전체를 훑습니다.
  2. 함수 내 존재하는 변수, 함수 선언에 대한 정보를 기억하고 실행합니다.
  3. 유효범위는 함수 블록 {} 내 인데 필요한 값들을 블록 위의 상단으로 끌어올리는 것입니다.
  4. 실제 코드가 끌어올려지는 것이 아니고 자바스크립트 parser가 내부적으로 끌어올려 처리하는 것이므로 실제 메모리에서는 변화가 없습니다.

<br />

- **var 선언문 호이스팅**

  ```jsx
  console.log(test); //undefined

  var test = 123;
  console.log(test); //123
  ```

  변수 test가 선언되기 전에 참조 시 에러가 발생하지 않고 undefined가 출력됩니다.

  이는 코드 실행 전에 자바스크립트 내부에서 미리 test변수를 선언하여 undefined로 초기화를 해두었기 때문입니다.

  따라서 var 키워드 변수는 호이스팅 과정에서 선언 및 초기화 단계가 동시에 진행됨을 알 수 있습니다.

    <br />

- **let / const  선언문 호이스팅**

  ```jsx
  console.log(test); //ReferenceError: a is not defined

  let test = 123;
  console.log(test); // 123
  ```

  같은 상황에서 let과 const의 경우 error를 발생시키는데 바로 TDZ(Temporal Dead Zone) 때문입니다.

  TDZ란 스코프 시작 지점 에서 초기화 시작 지점 까지를 말하는데 TDZ 영역에 있는 변수들은 사용을 할 수 없습니다.

  let과 const는 TDZ에 영향을 받기 때문에 할당을 하기 전에는 사용이 불가합니다.

  즉, let의 경우 선언 단계까지는 완료되었지만 초기화가 되지 않아 에러가 발생하는 것입니다.

  이는 잠재적인 버그를 줄일 수 있다는 장점이 있습니다.

    <br />

- **함수선언문 호이스팅**

  ```jsx
  test(); //test

  function test() {
    console.log("test");
  }
  ```

  함수 호출이 함수선언문의 위에 있든 아래쪽에 있든 함수 선언문은 호이스팅 영향으로 끌어올려지기 때문에 에러가 발생하지 않습니다.

<br />

- **함수표현식 호이스팅**

  ```jsx
  test(); // error

  var test = function () {
    console.log("test");
  };

  test(); // test
  ```

  함수 표현식의 경우 **선언, 초기화, 할당** 단계가 모두 동시에 진행됩니다.
  그래서 할당 전 호출해도 undefined이 아니라 함수 내용이 return 되기 때문에 위 와 같이 에러가 발생합니다.