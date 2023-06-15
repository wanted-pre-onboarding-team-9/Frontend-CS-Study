#  React state와 props에 대해 설명해 주세요.

state와 props 모두 컴포넌트 내부에서 사용되는 값들이다.

## State

일반적으로 컴포넌트 내부에서 지속적으로 변경이 일어나는 값을 관리하기 위해 사용한다.

사용자의 입력이나 개발자의 의도에 의해 상태가 변화할 수도 있다.

주로 `useState` Hook을 통해 반환되는 `setState` 함수를 활용하여 사용되며 변경된 값으로 재랜더링이 필요한 경우 React에 의해 자동으로 변경된 상태로 랜더링 한다.

```tsx
const Counter = () => {
	const [count, setCount] = useState<number>(0);
	
	const onClickHandler = () -> {
		// setCount(count + 1);
		setCount((prev) => prev + 1);
	}

	return (
		<div>
			<p>{ count }</p>
			<button onClick={onClickHandler}>ADD</button>
		</div>
	);

}
```

### `setState()`의 특징

1. **비동적으로 동작**
    
    React는 setState를 하나로 묶어 성능을 최적화하고, 한 번에 상태 업데이트를 처리하기 위해서 비동기로 동작하게 했다.
    
    동기로 동작했다면, setState마다 랜더링이 발생해서 성능상 문제가 생길 수 있다.
<br >
   
2. **Batch Update**
    
    React는 `Batch Update`를 사용한다는 큰 특이점이 있다. `Batch Update`는 여러 개의 setState를 모아서 한 번에 처리하는 방식을 말한다. 이를 통해서 중간에 발생하는 중복 랜더링을 최소화하고, 최적화된 방식으로 업데이트를 수행할 수 있다.
    
    `Batch Update`는 React의 내부적인 최적화 방식이기 떄문에 사용자가 직접 개입하여 최적화 할 필요가 없다.

<br >

3. **state를 변경하는 두가지 방법**
    ![](https://velog.velcdn.com/images/tkddn_dev8430/post/1eb77457-9ddd-4273-9e7d-49c7c5714303/image.png)

    
    ```tsx
    // 직전 상태를 사용하는 경우
    setCount((prev) => prev + 1);
    
    // 새로운 상태를 적용하는 경우
    setCount(newCount);
    ```
    
    **일반적인 업데이트 방법**을 사용하여 연속적인 업데이트를 수행하면
    
    ```jsx
    const countHandler = () => {
    	setCount(count + 1);
    	console.log(count);
    	setCount(count + 1);
    	console.log(count);
    	setCount(count + 1);
    	console.log(count);
    };
	```  

	![](https://velog.velcdn.com/images/tkddn_dev8430/post/468f31d8-aa2a-4b81-9dbb-c7803892c166/image.gif)
 
    count를 업데이트 코드가 3개가 있음에도 불구하고, count의 값이 1씩 올라가는 것을 확인할 수 있다.
    
    일반 업데이트 방식을 사용했을 때에는 **setState를 하는 시점의 count 값을 참조해서** 1이 된다.
    
    그리고 React에서는 Batch Upate가 이루어지기 때문에 나머지 setState 구문을 처리한  이후 실제 count의 값이 한 번 업데이트되고 랜더링 되는 것이다.  
    
	다음으로 **함수형 업데이트**를 사용해서 업데이트를 수행해보면
    ```tsx
    const countBatchHandler = () => {
      setCount((count) => count + 1);
      console.log(count);
      setCount((count) => count + 1);
      console.log(count);
      setCount((count) => count + 1);
      console.log(count);
    };
    ```

	![업로드중..](blob:https://velog.io/30dc6a2b-3394-4101-8761-7e1468e8e5ba)
   
    일반적인 업데이트 방식과 달리 의도한 것처럼 count의 값이 3씩 올라가는 것을 확인할 수 있다.

    함수형 업데이트 방식을 사용하면 setState의 콜백함수가 순차적으로 콜 스택에 쌓이게 되어 **이전 state값을 기반으로** +1씩 업데이트 되게 된다. 그리고 동일하게 나머지 setState구문을 실행한 후 일괄적으로 랜더링된다. 연속적으로 상태 업데이트를 해야할 때 유용하게 사용할 수 있다.

    > **console.log는 왜 같은 값을 찍어내죠?**
    > 
    > 
    > setState를 통해서 실제 state가 update되는 시점은 리랜더링되는 시점이기 때문에, console.log()가 호출되는 시점에는 변경되기 전 state를 찍어내게 된다.
    > 

<br >


## Props

`props`는 Properties의 줄임말이며, 컴포넌트에 어떤 값을 전달할 때 사용한다. Props를 활용하여 재사용 가능한 컴포넌트를 만들 수 있다.

`props`는 몇가지 특성을 가진다.

```tsx
// App.js
const App = () => {
	return (
		<Block data="1" />
	);
}

// Block.js
const Block = (props) => {
	return (
		<p>{ props.data }</p>
	);
}

```

- `props`는 상위 컴포넌트에서 가지고 있는 하위 컴포넌트로 데이터를 전달하며, **단방향성**을 가진다.
- 컴포넌트에서 `props`를 사용할 때 props를 수정해서는 안된다. props는 읽기 전용이다.
    
    → 컴포넌트는 입력값에 대해서 조작하지 않고, 항상 똑같은 값을 return해야하는 순수함수로 짜여져야하기 때문에 `props`를 조작하면 안된다.

<br >

## References

https://react.dev/learn/state-a-components-memory

https://choonse.com/2022/01/21/677/

[https://velog.io/@doh_0112/Batch-Update에-대해서](https://velog.io/@doh_0112/Batch-Update%EC%97%90-%EB%8C%80%ED%95%B4%EC%84%9C)

https://dev-yakuza.posstree.com/ko/react/props-state/

https://github.com/uberVU/react-guide/blob/master/props-vs-state.md
