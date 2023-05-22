# Reconciliation에 대해 설명해 주세요.

## 비교 알고리즘

### 엘리먼트 타입이 다른 경우

완전히 새로운 트리를 구축합니다.  
다음 예시는 모두 엘리먼트 타입이 다르다고 판단합니다.

- `<a>` → `<img>`
- `<Article>` → `<Comment>`
- `<Button>` → `<div>`

또한 아래의 예시에서 이전 `Counter`는 사라지고 새로 마운트됩니다.

```jsx
<div>
  <Counter />
</div>

<span>
  <Counter />
</span>
```

### DOM 엘리먼트 타입이 같은 경우

변경된 속성들만 갱신합니다.

아래 예시에서는 `className`만 수정이 일어납니다.

```jsx
<div className="before" title="stuff" />

<div className="after" title="stuff" />
```

`style`이 갱신될 경우 변경된 속성만을 갱신합니다.  
아래 예시헤서는 `color` 속성만 수정합니다.

```jsx
<div style={{color: 'red', fontWeight: 'bold'}} />

<div style={{color: 'green', fontWeight: 'bold'}} />
```

### 같은 타입 & 같은 위치의 컴포넌트

state를 유지하고 props를 갱신합니다.

중간에 `if`문을 사용하여 다른 위치에서 `return` 했다고 하더라도, React는 반환된 트리만 인식합니다.

만약 state를 유지하고 싶지 않다면 **key**를 이용할 수 있습니다.  
아래의 예시에서는 state가 초기화됩니다.

```jsx
{
  isPlayerA ? <Counter key="Taylor" person="Taylor" /> : <Counter key="Sarah" person="Sarah" />;
}
```

key를 위치의 일부로 사용하여 동일한 위치에 렌더링해도 다른 컴포넌트로 인식하기 때문입니다.

> 중첩된 컴포넌트 함수 선언은 하면 안 됩니다.  
> 매 렌더마다 함수가 생성되어 다른 컴포넌트로 인식하기 때문에  
> 원하지 않는 결과가 나올 수 있습니다.  
> [codesandbox](https://codesandbox.io/s/0p1vil?file=/App.js&utm_medium=sandpack)

<br>

## `ReconcileChildren`

아래는 [Build your own React](https://pomb.us/build-your-own-react/) 글을 보고 분석한 자식 재조정 과정입니다.  
관심있는 분들만 보셔도 무방합니다.

- **oldFiber** `fiber.alternate.child`
- **element** `fiber.props.children[index]`

1. oldFiber의 sibling을 돌면서 key가 있는 fiber들로 Map 생성
2. element에 key가 있다면  
   a. oldFiber의 key와 같을 경우 effectTag: “UPDATE”  
   b. 다를 경우 Map.get(element key)로 ❶에서 생성한 같은 key를 가졌던 fiber를 가져와서 있을 경우 effectTag: “PLACEMENT”
3. ❷ 과정에서 해당되는 게 없었다면 같은 타입일 경우 UPDATE, 다른 타입일 경우 PLACEMENT로 설정
4. oldFiber의 type과 element의 type이 다르다면 oldFiber “DELETION"

```js
const getKey = (fiber) => fiber && fiber.props && fiber.props.key;
function reconcileChildren(wipFiber, elements) {
  let index = 0;
  let oldFiber = wipFiber.alternate && wipFiber.alternate.child;
  let prevSibling = null;

  // oldFiber sibling을 돌면서 key가 있는 fiber Map 생성 ❶
  const keyFiberMap = createKeyFiberMap(oldFiber);

  while (index < elements.length || oldFiber != null) {
    const element = elements[index];
    let newFiber = null;
    const elementKey = getKey(element);
    if (elementKey) {
      const sameKey = getKey(oldFiber) === elementKey;
      if (sameKey) {
        // oldFiber와 key가 같다면 위치도 같으므로 UPDATE
        newFiber = {
          type: oldFiber.type,
          props: element.props,
          dom: oldFiber.dom,
          parent: wipFiber,
          alternate: oldFiber,
          effectTag: "UPDATE",
        };
      } else {
        // 같은 key를 가진 fiber가 있는지 확인
        const sameKeyFiber = keyFiberMap.get(elementKey);
        if (sameKeyFiber) {
          // 위치가 다르므로 PLACEMENT
          newFiber = {
            type: sameKeyFiber.type,
            props: element.props,
            dom: sameKeyFiber.dom,
            parent: wipFiber,
            alternate: sameKeyFiber,
            effectTag: "PLACEMENT",
          };
        }
      }
    }
    const sameType = oldFiber && element && element.type === oldFiber.type;

    if (!newFiber) {
      // key를 이용한 처리를 하지 않았다면 원래 동작 (❸)
      if (sameType) {
        newFiber = {
          type: oldFiber.type,
          props: element.props,
          dom: oldFiber.dom,
          parent: wipFiber,
          alternate: oldFiber,
          effectTag: "UPDATE",
        };
      }
      if (element && !sameType) {
        newFiber = {
          type: element.type,
          props: element.props,
          dom: null,
          parent: wipFiber,
          alternate: null,
          effectTag: "PLACEMENT",
        };
      }
    }

    // 이건 newFiber effectTag UPDATE 아니면 지워야됨 ❹
    if (oldFiber && !sameType) {
      oldFiber.effectTag = "DELETION";
      deletions.push(oldFiber);
    }

    if (oldFiber) {
      oldFiber = oldFiber.sibling;
    }
    if (index === 0) {
      wipFiber.child = newFiber;
    } else if (element) {
      prevSibling.sibling = newFiber;
    }

    prevSibling = newFiber;
    index++;
  }
}

function createKeyFiberMap(oldFiber) {
  const keyFiberMap = new Map();
  let currentFiber = oldFiber;
  while (currentFiber) {
    const key = getKey(currentFiber);
    if (key) {
      keyFiberMap.set(key, currentFiber);
    }

    currentFiber = currentFiber.sibling;
  }
  return keyFiberMap;
}
```

## 참고 자료

- [Preserving and Resetting State (react.dev)](https://react.dev/learn/preserving-and-resetting-state)
- [Reconciliation (react docs)](https://legacy.reactjs.org/docs/reconciliation.html)
- [Build your own React](https://pomb.us/build-your-own-react/)
