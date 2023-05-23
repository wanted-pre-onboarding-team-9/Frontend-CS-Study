## 고차 컴포넌트(HOC)는 무엇인가요?

고차 컴포넌트는 컴포넌트 로직을 재사용하기 위한 기술입니다.

각각 컴포넌트에서는 코드를 반복하지 않고, 공통 기능을 추가할 수 있도록 해줍니다.

예를 들어, UserPage와 TodoPage라는 두가지 컴포넌트가 있습니다.

간단하게 아래와 같이 코드를 작성할 수 있습니다.

```jsx
// UserPage.js
function UserPage() {
  return (
    <div>
      <h1>User Page</h1>
      <p>This is User Page...!</p>
    </div>
  );
}

export default UserPage;

// TodoPage.js
function TodoPage() {
  return (
    <div>
      <h1>Todo Page</h1>
      <p>This is Todo Page...!</p>
    </div>
  );
}

export default TodoPage;
```

두 컴포넌트는 각각 페이지 이름과, 페이지 설명을 가집니다.

하지만 컴포넌트의 구조가 동일하고 표현하는 데이터만 다르기 때문에 이것을 HOC를 통해 공통으로 처리할 수 있습니다.

화면에 표현되는 컴포넌트 구조는 그대로 각 컴포넌트에서 담당하고, HOC에서 여러 컴포넌트에서 다르게 처리할 데이터를 인자로 받음으로서 다르게 처리할 수 있게 해줍니다.

HOC를 적용해보면 다음과 같이 구조를 바꿀 수 있습니다.

```jsx
// withTitle.js
import React, { Component } from 'react';

function withTitle(WrappedComponent, pageTitle) {
  return class extends Component {
    render() {
      return (
        <div>
          <h1>{pageTitle}</h1>
          <WrappedComponent {...this.props} />
        </div>
      );
    }
  };
}

// UserPage.js
function UserPage(props) {
  return <p>This is User Page...!</p>;
}

const UserPageWithTitle = withTitle(UserPage, "User Page");

export default UserPageWithTitle;

// TodoPage.js
function TodoPage(props) {
  return <p>This is Todo Page...!</p>;
}

const TodoPageWithTitle = withTitle(TodoPage, "Todo Page");

export default TodoPageWithTitle;
```

withTitle이라는 HOC에 컴포넌트와, 각 컴포넌트마다 변경되는 값(pageTitle)을 넘겨 줌으로서 같은 구조를 가진 컴포넌트를 다른 데이터로 사용할 수 있습니다.

HOC를 활용하면 인증&인가나 데이터 호출 로직을 추가하여 공통으로 여러 컴포넌트에서 사용할 수 있게 해줍니다.

답변) HOC는 컴포넌트 로직의 재사용성을 높이기 위한 기술입니다. 고차 컴포넌트를 만들어 내부에서는 공통으로 처리할 로직을 작성하고, 컴포넌트를 매개변수로 전달받아 여러 컴포넌트로 하여금 공통적인 로직을 처리하게 끔 사용할 수 있습니다. 예를 들어 인증이 필요한 여러 컴포넌트들이 있다고 가정하면 인증 로직을 포함하는 withAuth라는 HOC를 제작하하고, 관련 컴포넌트를 호출할 때는 withAuth의 매개변수에 각각의 컴포넌트에 추가하는 방식을 통해 사용할 수 있습니다.

<br/>

### 추가) HOC vs Hook

로직을 재사용한다는 점 때문에, HOC는 마치 Hook이 어떤 차이가 있는지 궁금했습니다.

앞서 설명했듯 HOC는 컴포넌트를 함수의 매개변수로 전달되어, 기존 컴포넌트에 추가적인 기능을 제공하면서 동일한 컴포넌트를 랜더링합니다. 컴포넌트 사이에 인가/인증, 데이터 처리와 같이 공통으로 처리하는 로직을 공유하고, 컴포넌트마다 달라지는 데이터를 주입하는 관점에서 사용하는 기법이라고 생각합니다.

Hook은 클래스 컴포넌트가 아닌 함수형 컴포넌트라도 상태 로직을 재사용할 수 있게 해주는 역할을 합니다. 여러 컴포넌트의 내부에서 상태 로직을 사용할 수 있습니다.

HOC는 여러 로직에 대해서 유연하게 로직의 재사용성을 부여하는 관점을 가지고 있고, Hook은 상대적으로 상태관리와 React 라이프 사이클이나 이벤트에 좀 더 집중하고 있다는 차이점이 있습니다.
