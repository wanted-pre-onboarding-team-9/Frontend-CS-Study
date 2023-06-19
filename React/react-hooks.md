# React Hooks는 무엇인가요? 장점은 뭐가 있나요? 어떤 Hooks가 있는지 설명해주세요.

## React Hooks란?

Hook은 함수 컴포넌트에서 React state와 생명주기 기능(lifecycle features)을 “연동(hook into)“할 수 있게 해주는 함수입니다. Hook은 class 안에서는 동작하지 않습니다. 대신 class 없이 React를 사용할 수 있게 해주는 것입니다. (하지만 이미 짜놓은 컴포넌트를 모조리 재작성하는 것은 권장하지 않습니다. 대신 새로 작성하는 컴포넌트부터는 Hook을 이용하시면 됩니다.)
[공식문서 참고](https://ko.legacy.reactjs.org/docs/hooks-overview.html#but-what-is-a-hook)

## React hooks의 장점

1. 상태 관리의 용이성: Hooks를 사용하면 클래스 컴포넌트의 this.state 및 this.setState 대신 useState 훅을 사용하여 간단하게 상태를 관리할 수 있습니다. useState는 상태를 변경하고 컴포넌트를 다시 렌더링하는 데 필요한 모든 기능을 제공합니다.
2. 라이프사이클 메서드 대체: 이전에는 클래스 컴포넌트에서만 라이프사이클 메서드를 사용할 수 있었지만, Hooks를 사용하면 useEffect 훅을 통해 컴포넌트의 마운트, 언마운트, 업데이트 시점에서의 작업을 처리할 수 있습니다. useEffect는 컴포넌트의 생명주기와 관련된 로직을 훅 형태로 작성할 수 있도록 해줍니다.
3. 코드의 가독성과 재사용성: Hooks를 사용하면 상태와 라이프사이클 메서드 관련 로직을 컴포넌트 내에서 더욱 명확하게 분리할 수 있습니다. 이렇게 하면 코드의 가독성이 향상되고, 로직의 재사용성도 증가합니다. Custom Hook을 작성하여 여러 컴포넌트에서 재사용할 수 있는 로직을 구현할 수도 있습니다.
4. 클래스 컴포넌트와의 호환성: Hooks는 기존의 클래스 컴포넌트와 함께 사용할 수 있습니다. 기존에 작성한 클래스 컴포넌트를 전면적으로 수정하지 않고도 일부 컴포넌트에서 Hooks를 사용할 수 있습니다. 이를 통해 기존 프로젝트의 코드를 점진적으로 업그레이드할 수 있는 유연성을 제공합니다.
5. 테스트의 용이성: Hooks를 사용하면 상태 관리와 라이프사이클 메서드가 컴포넌트 외부로 분리되기 때문에 테스트하기가 더욱 용이해집니다. 상태 변경이나 특정 이벤트에 대한 행동을 단순한 함수로 테스트할 수 있으므로 테스트 코드의 작성과 유지보수가 간편해집니다.

## React hooks 종류

- useState : 상태 관리를 위한 훅으로, 컴포넌트 내에서 상태 값을 저장하고 변경할 수 있게 해줍니다.

```jsx
const [state, setState] = useState(initialState)
```

- useEffect : 컴포넌트의 라이프사이클 메서드 역할을 하는 훅으로, 컴포넌트가 마운트, 언마운트, 업데이트될 때 특정 작업을 수행할 수 있습니다.

```jsx
useEffect(() => {
  // 작업 수행
}, [dependency])
```

- useContext : React의 Context를 사용하기 위한 훅으로, 컴포넌트 트리에서 전역적으로 상태를 공유할 수 있게 해줍니다.

```jsx
const value = useContext(MyContext)
```

- useReducer: 복잡한 상태 관리를 위해 사용되는 훅으로, useState 대신 상태를 관리하고 업데이트하는 데 사용됩니다. useReducer를 사용하면 객체를 변경하고 업데이트하는 로직들이 외부에 있기 때문에 컴포넌트에서는 단순히 명령(dispatch)만 하면 됩니다. 그리고 로직들이 외부에 있기 때문에 재사용이 가능합니다.

```jsx
// reducer : 객체를 새롭게 만들어 나갈 로직을 작성한 함수를 전달해 줌
// dispatch : reducer를 호출해 줌(setState의 역할과 비슷)
const [state, dispatch] = useReducer(reducer, initialState)
```

- useCallback: 콜백 함수를 메모이제이션하여 성능을 최적화하는 훅으로, 특정 의존성이 변경되지 않는 한 이전에 정의된 콜백 함수를 재사용합니다.

```jsx
const memoizedCallback = useCallback(() => {
  // 콜백 함수 내용
}, [dependency])
```

- useMemo: 계산 비용이 많은 함수의 결과를 메모이제이션하여 성능을 최적화하는 훅으로, 의존성이 변경되지 않는 한 이전 결과를 재사용합니다.

```jsx
const memoizedValue = useMemo(() => {
  // 계산 비용이 많은 작업 수행
  return result
}, [dependency])
```

- useRef: 변수를 기억하고 유지하기 위한 훅으로, 컴포넌트의 렌더링 사이클 간에 변수를 유지할 수 있습니다.
  useRef를 호출하여 생성된 객체를 참조합니다. initialValue은 변수의 초기값으로 사용됩니다.
  useRef를 사용하여 변수를 유지하는 주요한 이유는 변수의 변경이 발생해도 컴포넌트가 다시 렌더링되지 않는다는 점입니다. useRef는 내부적으로 유지되는 값이 변경되더라도 React가 해당 컴포넌트를 다시 렌더링하지 않도록 도와줍니다. useRef로 생성된 객체는 컴포넌트의 렌더링과 관련된 상태 변경과 무관하게 유지됩니다. 이는 useRef로 생성된 변수의 값이 변경되어도 React에게 알려지지 않고, 컴포넌트가 다시 렌더링되지 않는다는 것을 의미합니다.

```jsx
const refContainer = useRef(initialValue)
```

- useLayoutEffect: useEffect와 유사하지만, 브라우저의 레이아웃이 업데이트 된 후에 실행되는 차이가 있습니다. 주로 DOM 요소의 크기나 위치를 가져올 때 사용됩니다.

```jsx
useLayoutEffect(() => {
  // 레이아웃에 관련된 작업 수행
}, [dependency])
```

## 참고

https://ko.legacy.reactjs.org/docs/hooks-overview.html <br/>
Chat-GPT
