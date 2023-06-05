**JSX**는 JavaScript 파일 내에서 HTML의 마크업을 사용할 수 있게 해주는 JavaScript의 구문이 확장된 형태이다.

기존 웹은 HTML은 화면의 컨텐츠, CSS는 컨텐츠의 디자인, JS는 페이지의 로직을 담당하면서 각 파일에 별도로 보관했지만, 웹이 사용자와 상호작용하면서 페이지의 로직이 화면의 컨텐츠에 영향을 주게 되어 JSX를 통해 화면을 조작하는 로직과, 컨텐츠를 표현하는 마크업을 함께 작성할 수 있게 되었다.

JSX는 HTML과 비슷해보이지만 몇가지 작성 규칙 때문에 조금 더 엄격하게 정보를 표현할 수 있다. 

### JSX 작성 규칙
1. **JSX로 작성한 요소는 단일 루트 Element를 반환한다.**
    
   구성 요소로 여러 개의 요소를 반환하기 위해서는 최상위에 단일 태그로 래핑되어 있어야 한다.
   ```html
    <h1>Todos</h1>
    <p>Show your todo!</p>
    <ul>
      ...
    </ul>
   ```
    
   HTML에서 위와 같은 구조를 JSX로 표현하려고 한다면 아래와 같이 모든 Element를 <div>와 같이 하나의 태그로 래핑해야 가능하다.
    
   ```jsx
    const Todos = () => {
    	return (
          <h1>Todos</h1>
          <p>Show your todo!</p>
          <ul>
            ...
          </ul>
    	);
    }
   ```
    
   필요에 따라 `Fragments`를 사용해서 마크업에 아무것도 남기지 않고 표현할 수 있다.
    
   ```jsx
    const Todos = () => {
    	return (
          <>
            <h1>Todos</h1>
            <p>Show your todo!</p>
            <ul>
              ...
            </ul>
          </>
    	);
    }
   ```
    
   💡 **Element를 하나로 래핑해야하는 이유**
    
   JSX는 일반적인 JavaScript 메서드인 React.createElement의 문법적 설탕이다. JSX는 실행될 때 브라우저가 이해할 수 있는 일반 JavaScript로 다시 컴파일 된다.
    
   예를 들어 JSX로 아래와 같이 작성했다고 한다면,
    
   ```jsx
    const Todo = () => {
    	return (
		    <div>
				<h1>Todo #2</h1>
             		<p className="todo-text">Go to gym</p>
           	</div>
    	)
    }
   ```
    
   JavaScript로 다음과 같이 똑같이 작성할 수 있다.
    
   ```jsx
    const Todo => () => {
    	return React.createElement(
    		'div',
    		{},
    		React.createElement('h1', {}, 'Todo #2'),
    		React.createElement('p', {className : 'todo-text'}, 'Go to gym'),
    	)
    }
   ```
    
   보는 것 처럼 하나의 React.createElement() 안에 하위 Element를 인자로 넘겨주면서 자녀, 손자 개념을 부여할 수 있다.
    
   만약에 Root Element로 감싸지 않은 경우에는
    
   ```jsx
    const Todo = () => {
    	return (
    		<h1>Todo #2</h1>
    		<p className="todo-text">Go to gym</p>
    	)
    }
    
    const Todo => () => {
    	return React.createElement('h1', {}, 'Todo #2'),
    		React.createElement('p', {className : 'todo-text'}, 'Go to gym'),
    	)
    }
    // ?????
   ```
    
   JSX가 일반 JS로 변환되면서 동시에 여러 개를 반환하려고 하지만 유효한 함수의 형태가 아니기 때문에 한 번에 여러 개를 return할 수 없다.
    
   그래서 JSX로 Element를 만드는 경우에 반드시 Root Element로 자식 Element를 래핑해야한다.
<br>

    
2. **모든 태그는 명시적으로 닫혀있어야 한다.**
    
   JSX에서는 모든 태그는 코드 상에서 명시적으로 닫혀있어야 한다.
    
   ex) `<img />` , `<li>Todo #1</li>`
<br>

    
3. **JSX로 작성된 요소의 속성은 camelCase를 따르고, 예약어는 사용할 수 없다.**
    
    아래 처럼 JSX는 브라우저 실행 이전에 bable을 통해 JavaScript 코드로 변환된다.
    
  ```jsx
  const Todo = () => {
      return (
          <div className='todo-unit'>
              <h1>Todo #3</h1>
              <p>Go to gym</p>
          </div>
      )
  }

  ```
  ```js
  import { jsx as _jsx } from "react/jsx-runtime";
  import { jsxs as _jsxs } from "react/jsx-runtime";
  const Todo = () => {
    return /*#__PURE__*/ _jsxs("div", {
      className: "todo-unit",
      children: [
        /*#__PURE__*/ _jsx("h1", {
          children: "Todo #3"
        }),
        /*#__PURE__*/ _jsx("p", {
          children: "Go to gym"
        })
      ]
    });
  };

  ```
    
참고) [babel 편집기](https://babeljs.io/repl/#?browsers=defaults%2C%20not%20ie%2011%2C%20not%20ie_mob%2011&build=&builtIns=false&corejs=3.21&spec=false&loose=false&code_lz=MYewdgzgLgBAKiAJiGBeGAKAlGgfDAbwCgBIAJwFMoBXMsTImJmEgHkQEsA3GYAGwCGECADkBAWwqoA5FCQgAtNTAco03I2Za2ACwCMuBMhgBiAMysA9Po1btrAA64A4ijkwA5gE9xVp5vtLTi5bZiwiAF8iaKIgA&debug=false&forceAllTransforms=false&modules=false&shippedProposals=false&circleciRepo=&evaluate=false&fileSize=false&timeTravel=false&sourceType=module&lineWrap=true&presets=react&prettier=true&targets=&version=7.22.4&externalPlugins=&assumptions=%7B%7D)
    
   우리가 작성한 JSX Element는 JavaScript의 객체로 바뀌고, Element의 속성은 JavaScript 객체의 `key: value` 형태로 저장 되어, 이후 속성이 필요할 때 읽어 사용된다. 이때 JS에서 사용되는 것을 생각하여 예약어를 사용할 수 없다. 
    
   ex) `className` , `onClick`
    
<br>

### Reference
https://dillionmegida.com/p/why-jsx-expressions-must-have-one-parent/  
https://ko.legacy.reactjs.org/docs/jsx-in-depth.html
