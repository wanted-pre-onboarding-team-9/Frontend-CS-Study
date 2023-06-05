## 명령형 vs 선언형 프로그래밍에 대해서 설명해주세요

명령형 프로그래밍은 프로그래밍의 상태와 상태를 변경시키는 구문의 관점에서 연산을 설명하는 프로그래밍이다. 컴퓨터가 수행할 명령을 순서대로 나열해놓은 형태를 보인다. 프로그램, 로직이 문제를 어떤 과정을 거쳐서, **어떻게** 해결할 것인가에 초점이 맞추어져 있다.

```jsx
function double (arr) {
  let results = [];
  for (let i = 0; i < arr.length; i++){
    results.push(arr[i] * 2);
  }
  return results;
}
```
<br>

### 선언형 프로그래밍

선언형 프로그래밍은 어떤 방법으로 컴퓨터가 동작할지 나타내는 것 보다 무엇을 할 것인지를 설명하는 프로그래밍. 프로그램이 **무엇을 수행할지에 초점**을 맞춘 프로그래밍 방식이다.

무엇을 화면에 보여줄지, 어떤 정보를 가져올지에 초점, 이때 가져오는 방식, 보여주는 방식은 **추상화** 되어있다. 선언형 방식으로 접근하기 위해서는 해당 내용이 ‘어떻게 문제에 접근하지’라는 명령적으로 먼저 추상화가 되어 있어야 한다.

```sql
SELECT * FROM Users WHERE User_Id ='N2929';
```

```html
<div>
  <h1>Declarative Programming</h1>
  <p>Sprinkle Declarative in your verbiage to sound smart</p>
</div>
```

```jsx
function double(arr) {
  return arr.map((item) => item * 2);
}
```
<br>

### React에서 선언형 프로그래밍

```jsx
// 선언형
const Todo = () => {
	const onClickTodo = () => {}
	const isHighlight = () => {}

	return (
		<div className='todo-unit'>
			<h1>Todo #3</h1>
			<p>Go to gym</p>
		</div>
	)
}

// 명령형
 const Todo => () => {
 	return React.createElement(
 		'div',
 		{className : 'todo-unit'},
 		React.createElement('h1', {}, 'Todo #3'),
 		React.createElement('p', {}, 'Go to gym'),
 	)
 }
```

> React는 상호작용이 많은 UI를 만들 때 생기는 어려움을 줄여줍니다. 애플리케이션의 각 상태에 대한 간단한 뷰만 설계하세요. 그럼 React는 데이터가 변경됨에 따라 적절한 컴포넌트만 효율적으로 갱신하고 렌더링합니다.
> 
> 
> 선언형 뷰는 코드를 예측 가능하고 디버그하기 쉽게 만들어 줍니다.
> 

React 공식문서에서도 선언형 프로그래밍을 활용한 라이브러리라고 설명하고 있다.


**💡 React가 선언형 프로그래밍을 사용했을 때의 이점**

1. 개발자는 무엇을 보여줄지(View)에만 집중하여 개발할 수 있다.
2. 비교적으로 간결한 코드로 개발가능하다.
3. 선언한 View 대로 결과가 나오기 때문에 결과를 예측하기 쉽다.
    → 실제로 View를 그리는 과정은 React 라이브러리가 담당한다.
    → React를 사용하는 사용자는 화면을 그리는 것에만 집중할 수 있고, React 자체의 성능, 랜더링 성능에 대한 것은 React 개발자들이 제공할 수 있도록 그부분에만 집중할 수 있다.
<br>

### Reference
https://ui.dev/imperative-vs-declarative-programming  
https://blog.mathpresso.com/declarative-react-and-inversion-of-control-7b95f3fbddf5  
https://medium.com/trabe/why-is-react-declarative-a-story-about-function-components-aaae83198f79 
