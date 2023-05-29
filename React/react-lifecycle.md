# 리액트에 있는 라이프사이클과 각 라이프사이클의 역할을 설명해주세요.

컴포넌트의 생명주기란 컴포넌트가 생성되고 렌더링되다가 소멸하는 과정을 의미합니다. 컴포넌트의 생명주기는 다음과 같은 세 가지의 단계로 구분됩니다.

1.  Mounting  
    컴포넌트는 화면에 나타날 때, 즉 가상 DOM 객체가 물리 DOM 객체로 바뀌는 시점에 마운트됩니다.
2.  Updating  
    state나 props가 변경될 때 업데이트 됩니다.
3.  Unmounting  
    컴포넌트가 물리 DOM 객체로 있다가 소멸하는 시점, 즉 화면에서 사라질 때 언마운트 됩니다.

# 클래스 컴포넌트의 생명 주기

![](https://blog.kakaocdn.net/dn/wEi13/btshwlT2OyZ/AJT9N3nGeBfeO8yukIOOvk/img.png)

## Mounting

### constructor()

- 클래스 컴포넌트가 마운트되기 전에 실행됩니다. state를 선언하고 메서드를 바인딩합니다.

### render()

- JSX를 HTML로 변환하여 화면에 보여주는 메서드입니다.

### ComponentDidMount()

- 컴포넌트 내에서 렌더링이 된 이후에 실행되는 메서드로, `setTimeout`, `setInterval`, 네트워크 요청 같은 비동기 작업을 처리할 때 사용됩니다.
- `componentDidMount`를 사용할 경우 `componentDidMount`에서 수행한 작업을 정리하기 위해 `componentDidUpdate`, `componentWillUnmount`를 함께 사용해야 합니다.

## Updating

### componentDidUpdate()

- props 또는 state가 변하여 리렌더링 되는 경우에 호출되며, 초기 렌더링에 대해서는 호출되지 않습니다.

## Unmounting

### componentWillUnmount()

- 컴포넌트가 화면에서 사라지기 전에 호출되는 메서드입니다.

# 함수 컴포넌트의 생명 주기

![](https://blog.kakaocdn.net/dn/cNO87f/btshxUCLQkN/KCtBEjb09xnVouK4ztNhw0/img.png)

## Mounting

### function() {} (컴포넌트 내부)

- 가장 먼저 컴포넌트 내부가 호출되어, 클래스 컴포넌트의 `constructor()`와 비슷하게 state나 함수를 정의하는 공간입니다.
- 라이프 사이클 메서드에 포함되지는 않습니다.

### return()

- JSX를 HTML로 변환하여 화면에 보여주는 메서드입니다.
- props와 state 값에 접근은 가능하지만, setState() 사용은 불가능합니다.

## useEffect(function, dependencies?)

- `Mounting`, `Updating`, `Unmounting`이 가능한 메서드입니다.useEffect(()=>{})
- 화면이 렌더링 된 이후 실행되며, 렌더링될 때마다 다시 실행됩니다.useEffect(()=>{},\[\])
- `dependencies`에 빈 배열을 설정하면 화면이 렌더링 된 이후 한 번만 수행됩니다.useEffect(()=>{},\[a\])
- 화면이 렌더링 된 이후 실행되며, `dependencies`에 넣은 값이 변경될 경우 수행됩니다.function에 return 추가
- 컴포넌트가 unmount될 때 실행됩니다.

> 참고 <br/> > [componentDidMount()](https://react.dev/reference/react/Component#componentdidmount)  
> [All Lifecycles in Class Components (Stateful) and Similar in Functional Components (Stateless) With Practical Tips in React JS](https://medium.com/swlh/all-lifecycles-in-class-components-stateful-and-similar-in-functional-components-stateless-c88564e42f24)  
> [\[React\] 클래스 컴포넌트 생명주기(lifecycle) 이해하기](https://adjh54.tistory.com/42)  
> [Class Component Lifecycle](https://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/)  
> [React Hooks Lifecycle](https://wavez.github.io/react-hooks-lifecycle/)
