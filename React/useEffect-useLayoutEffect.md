## useEffect

> 💡 외부 시스템과 컴포넌트를 동기화 할 수 있게 해주는 React Hook.

useEffect는 함수형 컴포넌트 생애 주기에서 화면이 랜더링(Rendering)되고 페인팅(Painting)된 이후에 **비동기적으로 실행**된다.

랜더링 이후 실행되기 때문에 useEffect내부에 DOM에 영향을 주는 코드가 있을 경우 사용자 입장에서 깜빡임을 경험하게 된다.

<br>

## useLayouEffect

> 💡 브라우저가 화면을 다시 그리기 전에 useEffect를 실행하는 버전입니다.

useLayoutEffect는 컴포넌트가 랜더링 된 이후에 실행되고, useLayoutEffect가 실행된 이후에 페인팅이 수행된다. useLayoutEffect는 **동기적으로 실행**된다. 페인팅 이전에 실행되기 때문에 DOM 조작이 있더라도 화면 깜빡임이 발생하지 않는다.

> **Render** - DOM Tree를 구성하기 위해 각 엘리번트의 스타일 속성을 계산
>    **Paint** - 실제 스크린에 계산한 Layout을 표시하고 업데이트 하는 과정

<br>

## Why useLayoutEffect?

> 💡 공식문서에서도 useLayoutEffect를 사용하면 성능상 저하가 있을 수 있다고 설명한다.


useLayoutEffect는 위치가 정해지지 않고 상황에 따라 바뀌는 컴포넌트에 대해서 사용할 수 있다.

| 최상단 컴포넌트의 툴팁 | 나머지 컴포넌트 툴팁 |
|:-:|:-:|
|![](https://velog.velcdn.com/images/tkddn_dev8430/post/9e0de8bf-4f75-400b-9fe0-2197d4e966bf/image.png)|![](https://velog.velcdn.com/images/tkddn_dev8430/post/cc47b700-ad2d-46e8-89e9-ea351be18fc4/image.png)|






**두 사진을 보면 툴팁의 방향이 컴포넌트(버튼)의 위치에 따라 달라진다.**

툴팁의 위치를 계산하는 과정이 useEffect 내에서 처리되게 되면, 페인팅이 끝난 시점에서 툴팁의 위치가 계산되고,
그에 따라 컴포넌트의 위치를 다시 조절해야하기 때문에 재랜더링이 발생할 수 있다.

이때 useLayoutEffect를 사용하면, useLayoutEffect의 내부 동작(예를 들어, 컴포넌트의 위치를 계산)을 수행한 후, React가 DOM을 업데이트하여 브라우저에 표현한다.

| 최상단 컴포넌트의 툴팁 | 나머지 컴포넌트 툴팁 |
|:-:|:-:|
|![](https://velog.velcdn.com/images/tkddn_dev8430/post/903fbfc2-bf8a-4b4f-98a8-0be045a504fb/image.gif)useEffect (출처: [React 공식문서](https://react.dev/reference/react/useLayoutEffect#usage))|![](https://velog.velcdn.com/images/tkddn_dev8430/post/46d8e91e-56f7-4aa8-9c33-b389f05edffc/image.gif)useLayoutEffect (출처: [React 공식문서](https://react.dev/reference/react/useLayoutEffect#usage))|

내부동작을 수행할 때, useLayoutEffect는 **동기적으로** 실행되기 때문에 모든 상태 업데이트가 끝나는 것을 보장한다.
따라서 useLayoutEffect이후 실행될 painting을 차단한다.

useEffect에 비해 성능상의 이슈가 있다는 점도, 내부 상태 업데이트 로직이 동기적으로 수행되기 때문에 특별한 경우를 제외하고 사용을 지양하는 것 같다. useEffect에서 처리하는 상태 업데이트 로직이 클수록, useEffect에 비해 저하된 성능을 보여주게 된다.

<br>

### **정리하면,**

 다른 컴포넌트에 영향을 받아 결정하고 싶거나, 랜더링 시점에서 컴포넌트의 위치를 특정할 수 없는 경우, 컴포넌트의 위치를 계산하고, 이후에 화면을 업데이트 해주어야 한다.

useEffect를 사용하면 컴포넌트를 실제 그리는 과정(페인팅) 이후에 계산 로직이 수행되기 떄문에 초기 위치에서 실제 계산된 위치가 다를 경우, 컴포넌트 자체가 깜빡이는 현상이 발생할 수 있다.

하지만 useLayoutEffect의 경우 페인팅 과정 이전에 **동기적으로** 계산 로직을 수행하기 때문에 페이팅 시점에서는 계산된 위치를 사용하게 되어, 자연스럽게 컴포넌트가 화면에 그릴 수 있다.

useLayoutEffect는 useEffect와 달리 동기적으로 상태 업데이트를 수행하기 때문에, useEffect 내부 로직이 복잡할 수록 상대적으로 성능이 저하될 수 있어 사용을 지양하고 있다.

<br>

### Reference

React 공식문서 : [useEffect](https://react.dev/reference/react/useEffect)

React 공식문서 : [useLayoutEffect](https://react.dev/reference/react/useLayoutEffect)

Medium 블로그 : [[React] useEffect 와 useLayoutEffect 의 차이는 무엇일까?](https://medium.com/@jnso5072/react-useeffect-%EC%99%80-uselayouteffect-%EC%9D%98-%EC%B0%A8%EC%9D%B4%EB%8A%94-%EB%AC%B4%EC%97%87%EC%9D%BC%EA%B9%8C-e1a13adf1cd5)
