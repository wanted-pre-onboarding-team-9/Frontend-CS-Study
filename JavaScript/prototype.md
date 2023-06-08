## **[** 프로토타입(prototype) 이란? **]**

- 자바스크립트에서 모든 객체는 프로토타입을 가지는데 프로토타입은 객체를 만들기 위한 기본 틀이라고 할 수 있으며, 객체의 메서드나 프로퍼티를 상속받는 데 사용된다.

<br />
<br />

- 상속이란?
  자바스크립트는 프로토타입을 기반으로 상속을 구현하는데 여기서 상속이란 어떤 객체의 프로퍼티 또는 메서드를 다른 객체가 상속 받아 그대로 사용할 수 있는 것을 말하며 이를 통해 불필요한 중복을 제거한다.

<br />
<br />

```jsx
function Test(name) {
  this.name = name;
}

Test.prototype.introduce = () => {
  return `안녕하세요. ${this.name}입니다!`;
};

const test1 = new Test("JavaScript");
const test2 = new Test("React");

console.log(test1.introduce === test2.introduce);
// true
```

> Test 생성자 함수의 prototype 프로퍼티로 프로토타입에 접근하여 공유 메서드 introduce 를 생성했다. 그리고 Test 생성자 함수가 생성한 모든 인스턴스는 부모 객체 역할을 하는 프로토타입 Test.prototype 으로부터 introduce 메서드를 상속받는다.

<br />

즉! name 과 같이 개별적으로 소유하는 프로퍼티만 개별적으로 소유하고, 내용이 동일한 메서드는 프로토타입 상속을 통해 공유하여 사용한다.

이처럼, 프로토타입은 객체 간 상속을 구현하기 위해 사용되며, 부모의 역할을 하는 객체로서 다른 객체에 공유 프로퍼티 , 메서드를 제공한다.

<br />
<br />

- **프로토타입 체인**
  <br />
  모든 객체는 프로토타입의 계층 구조인 **프로토타입 체인**에 묶여있다.

<br />

```jsx
function Test(name) {
  this.name = name;
}

Test.prototype.introduce = () => {
  return `안녕하세요. ${this.name}입니다!`;
};

const test1 = new Test("JavaScript");
console.log(test1.hasOwnProperty("name"));
```

자바스크립트 엔진은 객체의 프로퍼티에 접근하려고 할 때 해당 객체에 접근하려는 프로퍼티가 없다면 접근자 프로퍼티가 가리키는 참조를 따라 부모 역할을 하는 프로토타입의 프로퍼티를 순차적으로 검색하는데 이를 프로토타입 체인이라고 한다.
