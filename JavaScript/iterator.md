# Iterator에 대해 설명해주세요.

아래 예시 코드처럼 ES6에서 추가된 문법인 for of를 사용하면 좀 더 선언적인 코드를 작성할 수 있고, length등의 데이터에 의존하지 않고 배열 자체로 순회가 가능합니다. 이것이 가능한 이유는 **iterable interface** 덕분이고, iterable inteface는 세가지로 구성되어 있습니다.

```jsx
// 배열의 길이, index에 의존해 순회
const arr = [1, 2, 3];

for (let i = 0; i < arr.length; i++) {
  const element = arr[i];
  console.log(element);
}
```

```jsx
// 배열 자체를 순회
const arr = [1, 2, 3];

for (const element of arr) {
  console.log(element);
}
```

1. **Iterable**

   **Iterable 객체**는 `@@iterator`의 실제 구현체인 `Symbol.iterator`라는 메서드를 가지고있는 객체입니다. 이 메서드가 **iterator**를 반환합니다.

   ![image](https://github.com/wanted-pre-onboarding-team-9/Frontend-CS-Study/assets/111125577/15df65ff-1ba5-48df-8b51-464ef253d3b6)

   배열의 메서드 values()가 `Symbol.iterator`의 프로퍼티로 나오는데, values()를 호출시켜보면 values() 메서드가 **iterator** 객체를 반환하는 함수임을 알 수 있습니다.

   ![image](https://github.com/wanted-pre-onboarding-team-9/Frontend-CS-Study/assets/111125577/f5432834-40ca-4ff5-bda4-60c940ce74a7)

2. **Iterator**

   **Iterator**는 **IteratorResult**를 반환하는 `next` 메서드를 가지고있는 객체입니다. `next` 메서드는 순차적으로 원소들을 탐색하며, `next` 메서드 호출시마다 새로운 객체를 반환합니다.

3. **IteratorResult**

   **IteratorResult**는 Boolean값을 갖는 `done`과 모든 타입의 값을 가질 수 있는 `value` 프로퍼티를 갖습니다. `value`에는 최근 순회 요소인 다음 시퀀스의 값이 담기고 `done` 프로퍼티에는 순회 완료 여부가 담겨 탐색이 완료될 때 값이 true가 됩니다.

   ![image](https://github.com/wanted-pre-onboarding-team-9/Frontend-CS-Study/assets/111125577/1185d89e-e99c-4f53-abab-7401a63c103e)
   ![image](https://github.com/wanted-pre-onboarding-team-9/Frontend-CS-Study/assets/111125577/4f9cfac4-24bd-4407-b323-f290ac6a14f2)

## References

[Iterators and generators - JavaScript | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Iterators_and_generators) <br />
[Iterator - JavaScript | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Iterator)
