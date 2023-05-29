# 제어 컴포넌트와 비제어 컴포넌트 설명해주세요.

React에서의 제어 컴포넌트(Controlled Component)와 비제어 컴포넌트(Uncontrolled Component)는 폼 요소(form element)에 대한 데이터 흐름 및 상태 관리 방식을 설명하는 개념입니다.

## 제어 컴포넌트(Controlled Component)란?

제어 컴포넌트는 state를 사용하여 폼 요소의 값을 제어하고 업데이트하는 방식을 말합니다.
이 방식에서는 값이 state에 의해 제어되므로 React 컴포넌트는 폼 요소의 현재 값을 항상 알고 있습니다. 값이 변경될 때마다 상태가 업데이트되며, 이러한 업데이트는 주로 onChange 이벤트 핸들러를 통해 수행됩니다. 주로 유효성 검사 등에서 사용할 수 있습니다.

## 비제어 컴포넌트(Uncontrolled Component)란?

state를 사용하지 않고 DOM 자체에 의해 폼 요소의 값이 관리되는 방식을 말합니다. 이 방식에서는 React 컴포넌트가 폼 요소의 값을 직접 제어하지 않으며, 일반적으로는 ref를 사용하여 폼 요소에 접근하여 값을 가져오거나 업데이트합니다.

## 제어 컴포넌트와 비제어 컴포넌트 차이점

제어 컴포넌트의 경우 값은 항상 최신값을 유지하며 사용자가 입력을 하는 액션을 취할때마다 리렌더링을 발생시키고 상태를 새롭게 갱신하는데, 이는 데이터와 UI에서 입력한 값이 항상 동기화됨을 알 수 있습니다.
반면, 비제어 컴포넌트는 사용자가 직접 트리거 하기 전까지는 리렌더링을 발생시키지도 않고 값을 동기화 시키지도 않습니다.

그렇기때문에 제어컴포넌트와 비제어컴포넌트는 각각 용도와 상황에 맞게 사용하면 될것 같습니다.

제어 컴포넌트 사용 : 즉각적으로, 실시간으로 값에 대한 피드백이 필요할 경우 <br/>
비제어 컴포넌트 사용 : 즉각적인 피드백이 불필요하고 제출시에만 값이 필요하다, 불필요한 렌더링과 값 동기화가 싫은 경우

## 추가 질문

Q. 비제어 컴포넌트가 불필요한 렌더링과 값의 동기화를 안일으키는 useRef를 사용하는데 useRef는 왜 리렌더링을 발생시키지 않는걸까요?

A. useRef의 경우 일반적인 자바스크립트 객체로서 메모리 heap에 저장되므로, 항상 같은 메모리 주소를 참조하여 컴포넌트가 아무리 리렌더링 되더라도 이미 저장된 값 자체는 삭제되지 않고, 컴포넌트의 변경사항을 감지할 수 없어서 리렌더링을 하지 않습니다.

## 참고

https://velog.io/@yukyung/React-%EC%A0%9C%EC%96%B4-%EC%BB%B4%ED%8F%AC%EB%84%8C%ED%8A%B8%EC%99%80-%EB%B9%84%EC%A0%9C%EC%96%B4-%EC%BB%B4%ED%8F%AC%EB%84%8C%ED%8A%B8%EC%9D%98-%EC%B0%A8%EC%9D%B4%EC%A0%90-%ED%86%BA%EC%95%84%EB%B3%B4%EA%B8%B0 <br/>
https://dev-note-97.tistory.com/314 <br/>