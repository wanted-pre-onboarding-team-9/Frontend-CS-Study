# 순수함수

## 순수함수란?

순수 함수는 동일한 인자가 들어갈 경우 **외부의 영향을 받거나, 외부에 영향을 주지 않고 항상 같은 값을 return 하는 함수**를 말한다.

```jsx
// 순수함수 O
const func1 = (first, second) => {
	return first + second;
}

console.log(add(1, 2)) // 3
console.log(add(2, 4)) // 6
console.log(add(2, 6)) // 8

// 순수함수 X --> 인자로 들어온 값 이외의 값에 의해 결과값이 변경된다.
let exteranlValue = 10;

const func2  = (first, second) => {
	return first + seconde + externalValue;
}

console.log(add(1, 2)) // 13

externalValue = 1;
console.log(add(1, 2)) // 4

// 순수함수 X --> 외부의 값에 영향을 준다.
let exteranlValue = 10;
const func3 = (first, second) => {
	externalValue = first;

	return first + second + exteranlValue;
}

console.log('before externalValue', externalValue); // 10
console.log(add(1, 2)) // 13
console.log('after externalValue', externalValue); // 1

// 순수함수 O --> 기존 값이 아닌 기존 값을 복사한 새로운 값을 return
let externalObject = { value: 10 }
const func4 = (first, second) => {
	return { value : externalObject + first + second }
}

console.log(func4(1, 2)); // { value: 13 }
```

<br />

## React에서 순수함수

React에서는 순수함수를 활용하여 컴포넌트를 구성하는 것을 추구한다.

React 공식문서에도 **‘모든 React 컴포넌트는 자신의 Props를 다룰 때 반드시 순수 함수처럼 동작해야 합니다’**라고 언급되어 있다.

<br />

### 왜 순수함수여야 하는가

React에서는 컴포넌트를 순수함수로 작성함으로서 다음과 같은 이점을 가져올 수 있다.

- **예측 가능하다**
    
    순수함수의 정의에 따라 만들어진 컴포넌트는 동일한 Props를 전달 받으면 동일한 결과를 전달하기 때문에 예측 가능하다.
    
- **테스트에 용이하다.**
    
    테스트에 영향을 주는 요인이 Props에 따라 동일한 결과를 전달하기 때문에 테스트에 용이하다.
    
- **성능 최적화가 가능하다.**
    
    순수함수로 작성된 컴포넌트의 경우 Props가 변경되지 않은 경우에 랜더링을 건너뛸 수 있기 때문에 성능 최적화가 가능하다.
  
<br />  

React에서 순수함수를 권장하지만 순수함수를 만들 수 없는 경우가 있다.

- **외부 데이터에 의존하는 경우**
    
    API 호출을 통해 외부 데이터에 영향을 받는 경우 데이터에 따라 컴포넌트가 영향을 받기 때문에 순수함수라고 볼 수 없다.
    
- **브라우저 이벤트에 의존하는 컴포넌트**
    
    브라우저 이벤트에 의해서 컴포넌트를 조작하는 것도 부작용이 발생할 수 있기 때문에 순순함수로 작성할 수 없다. 브라우저 이벤트는 예측 불가능해서 이벤트에 대한 처리를 항상 동일한 결과를 처리하게끔 할 수 없다.
    

위 두 경우를 가지는 컴포넌트는 상태관리 라이브러리를 통해 순수함수의 정의에 어긋나는 로직을 따로 분리하는 방식을 사용해 볼 수 있다.
