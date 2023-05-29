MDN에서는 함수와 그 함수가 선언됐을 때의 렉시컬 환경의 조합이라고 말합니다.  
좀 더 쉽게는 자신이 생성될 때의 외부 환경을 기억하고, 그를 사용하는 함수라고 할 수 있습니다.  
함수를 일급 객체로 취급할 경우 나타나는 현상, 특성으로 자바스크립트에 국한된 개념은 아닙니다.

> **일급객체**  
> 다른 객체들에 일반적으로 적용 가능한 연산을 모두 지원하는 객체를 가리킨다. 보통 함수에 인자로 넘기기, 수정하기, 변수에 대입하기와 같은 연산을 지원할 때 일급 객체라고 한다. - 위키백과

## 원리

### LexicalEnvironment

실행 컨텍스트의 구성 요소 중 하나로, 식별자와 값, 상위 스코프에 대한 참조를 기록하는 객체입니다.  
실행 컨텍스트와는 별개의 객체이기 때문에 해당 객체의 참조 카운트가 0이 아니라면 GC 대상이 되지 않습니다.

자바스크립트 엔진이 함수 정의를 평가하여 함수 객체를 전역 객체에 생성할 때 실행 중인 컨텍스트의 LexicalEnvironment를 함수 객체의 내부 슬롯`[[Environment]]`에 저장합니다.

함수가 호출되어 함수 실행 컨텍스트가 생성되면 OuterEnvironmentRecordReference는 함수 객체의 내부 슬롯`[[Environment]]`의 값을 참조하게 됩니다.

> 내부 슬롯  
> ECMA-script 명세에서 해당 명세에 따르는 자바스크립트 구동 엔진이 구현해야 하는 동작을 추상화시켜 설명하는 일종의 Pseudo Code

```js
function foo() {}

foo();
```

```js
// 이해를 돕기 위한 전역 객체
const global = {
  foo: {
    [[Environment]]: GlobalExecutionContext.GlobalLexicalEnvironment
  }
}

// 이해를 돕기 위한 함수 실행 컨텍스트
const FooFunctionExecutionContext = {
  LexicalEnvironment: {
    FunctonEnvironmentRecord: { ... },
    OuterEnvironmentReference: global.foo[[Environment]],
  },
};
```

따라서 외부 함수의 실행 컨텍스트 내에서 정의된 내부 함수가 외부 함수의 LexicalEnvironment를 참조하고 있다면 소멸하지 않게 되는 것입니다.

## 활용 예시

- **상태 기억**
- **상태 은닉**  
  이미 제거된 실행 컨텍스트의 LexicalEnvironment는 클로저 외에는 접근 방법이 없으므로 정보의 은닉이 가능합니다.
- **상태 공유**

## 실제 활용

React의 `useState`, `useEffect`를 클로저의 개념을 이용해 구현해 봅시다.

### `useState`

**❶ initialValue를 받아 그대로 state로 반환**

```js
export const { useState } = function makeMyHooks() {
  function useState(initialValue) {
    const state = initialValue;
    const setState = () => {};

    return [state, setState];
  }

  return { useState };
};
```

**❷ 초기 렌더링 이후에서는 기억한 state를 반환**

상태를 기억하기 위해 클로저를 이용합니다.

```js
export const { useState } = (function makeMyHooks() {
  // 몇 번째 훅인지 index를 이용해 관리
  let hookIndex = 0;
  const hooks = [];

  function useState(initialValue) {
    // || 연산자 사용 시 boolean state 관리 시 문제가 발생할 수 있어 ?? 연산자 사용
    const state = hooks[hookIndex] ?? initialValue;
    hooks[hookIndex] = state;
    hookIndex += 1;
    ...
  }
})
```

**❸ `setState` 구현**

1. state를 변경한다.
2. 다시 렌더링한다.

2의 경우 리액트와 관련된 요구사항이므로 자세히 다루지 않고, render 함수를 만들고 호출하는 식으로 해결하였다는 것만 참고 부탁드립니다.

```js
...
function useState(initialValue) {
  ...
  const setState = (newState) => {
    hooks[hookIndex] = newState;
    render();
  }
  ...
}
```

위와 같이 구현할 경우 `hookIndex`는 공유되는 값이기 때문에 증가된 상태이므로 문제가 발생합니다.

따라서 값을 고정하기 위해 클로저를 사용하겠습니다.

```js
...
function useState(initialValue) {
  ...
  const setState = function() {
    const currentIndex = hookIndex;
    return (newState) => {
      hooks[currentIndex] = newState;
      render();
    }
  }
  ...
}
```

이제 `currentIndex`는 `useState`가 호출될 때의 `hookIndex` 값으로 고정됩니다.  
렌더링 이후에는 `hookIndex` 값이 초기화되므로, 클로저를 이용하지 않고 `setState` 내에서 `currentIndex`를 저장해도 동일한 결과를 얻을 수 있습니다. `currentIndex`의 경우 `setState`에서만 사용하는 값이기 때문에 스코프를 좁혀 관리하고 싶다면 클로저를 이용하면 되겠습니다.

하지만 또 다른 문제가 있습니다. `hookIndex`가 다시 렌더링되어도 초기화되지 않기 때문에 배열이 계속 늘어나는 문제가 발생합니다.

이를 해결하기 위해 렌더링 전 `hookIndex`를 초기화하는 코드를 추가합니다.

```js
...
return (newState) => {
  hooks[currentIndex] = newState;
  hookIndex = 0;
  render();
}
...
```

### `useEffect`

요구 사항은 다음과 같습니다.

1. 처음 호출
2. dependencies(array)에 담긴 값이 변경될 경우
3. dependencies가 주어지지 않았을 경우

위 세 가지 경우에서 `effect` 함수를 호출합니다.

```js
export const { useState, useEffect } = (function makeMyHooks() {
  ...
  function useEffect(effect, dependencies) {
    const prevDeps = hooks[hookIndex];
    const isFirstCall = prevDeps === undefined; // 1
    const isDepsNotProvided = () => dependencies === undefined; // 3
    const hasDepsChanged = () => dependencies.some(
      (dep, index) => dep !== prevDeps[index]
    ); // 2

    if (isFirstCall() || isDepsNotProvided() || hasDepsChanged()) {
      effect();
    }

    hooks[hookIndex] = dependencies;
    hookIndex += 1;
  }

  return { useState, useEffect };
})
```

함수로 작성한 이유는 `dependencies`가 주어지지 않았을 경우를 고려하여 실행을 늦추기 위함입니다. `||` 연산자는 `true`가 나올 경우 뒤 코드가 호출되지 않는 것을 이용하여 실행을 지연시킨 것입니다. optional chaining operator`?.`를 사용해도 무방합니다.

### Hooks 사용 규칙

위와 같이 클로저를 이용한 구현 방법으로 인해 아래 규칙이 생겨났습니다.

> 최상위(at the Top Level)에서만 Hook을 호출해야 합니다. 반복문, 조건문 혹은 중첩된 함수 내에서 Hook을 호출하지 마세요. 이 규칙을 따르면 컴포넌트가 렌더링 될 때마다 항상 동일한 순서로 Hook이 호출되는 것이 보장됩니다.
