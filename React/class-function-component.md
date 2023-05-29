# 클래스 컴포넌트와 함수 컴포넌트의 차이는 무엇인가요?

## JSX 렌더링 방법

클래스 컴포넌트는 `render()` 메서드를 이용하여 JSX를 렌더링합니다.

```js
import React from 'react'

class ClassComponent extends React.Component {
  render() {
    return <h1>Class Component</h1>
  }
}
```

함수 컴포넌트는 JSX를 리턴합니다.

```js
import React from 'react'

const FunctionComponent = () => {
  return <h1>Function Component</h1>
}
```

## props 전달 방법

클래스 컴포넌트는 `this` 키워드를 사용합니다.

```js
class ClassComponent extends React.Component {
  render() {
    const { name } = this.props;
    return <h1>{ name }</h1>;
 }
```

함수 컴포넌트는 함수의 인자로 전달합니다.

```js
const FunctionComponent = (props) => {
  return <h1>{props.name}</h1>
}
```

## state 관리 방법

클래스 컴포넌트는 `this.state`를 사용하여 state를 관리합니다. state의 변경은 setState를 이용하여 할 수 있습니다.

```js
class Counter extends Component {
  state = {
    age:1

  handleChangeAge = () => {
    this.setState({
      age:this.state.age +1
    })
  }
}
```

함수 컴포넌트에서는 useState를 이용하여 같은 동작이 가능합니다.

```js
const [age,setAge] = useState(1)

function handleChangeAge {
  setAge(age+1)
}
```

## Lifecycle 관리 방법

클래스 컴포넌트는 Lifecycle API와 state 기능을 사용하여 상태를 관리합니다. Lifecycle API는 컴포넌트의 생성, 업데이트, 소멸과 같은 단계에서 실행되는 메서드들을 제공합니다. 이를 통해 컴포넌트의 동작을 제어하고 상태를 업데이트할 수 있습니다.

함수 컴포넌트는 hook을 사용하여 Lifecycle API와 state를 관리합니다.

<br/>

### 클래스 컴포넌트와 함수 컴포넌트를 어떤 경우에 사용하면 좋을까?

[공식 문서](https://react.dev/reference/react/Component#alternatives)에는 클래스 컴포넌트를 계속 지원하지만 추천하지는 않는다고 언급하고 있습니다. <br/>
다만 `getSnapshotBeforeUpdate`, `getDerivedStateFromError`, `componentDidCatch` 메서드에 해당하는 hook이 없기 때문에 이런 메서드가 필요한 경우에는 예외적으로 클래스 컴포넌트를 작성하는 것이 좋습니다.
[(참고)](https://react.dev/reference/react/Component#getsnapshotbeforeupdate)
