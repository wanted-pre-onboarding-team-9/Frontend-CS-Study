# css selector 우선순위를 말해주세요

## css selector 우선순위

**1순위 !important (중요성의 원칙 적용)**

```css
p {
  color: red !important;
}
```

**2순위 inline style**

```html
<p style="color: red"></p>
```

**3순위 id Selector**

```html
<p id="title">제목</p>
```

```css
#title {
  color: red;
}
```

**4순위 class Selector**

```html
<p class="subtitle">부제목</p>
```

```css
.subtitle {
  color: red;
}
```

**5순위 tag Selector(요소 선택자)**

```css
p {
  color: red;
}
```

**6순위 universal Selector(전체 선택자)**

```css
* {
  color: red;
}
```

<br/>

## 선택자 우선순위 3가지 원칙

1. 후자 우선의 원칙
2. 구체성(=명시도)의 원칙
   2-1. 가중치
3. 중요성의 원칙
   <br/>

- 어떤 선택자가 더 구체적인가?를 판단할때 **가중치**를 기준으로 판단합니다.<br/>
  → id > class > tag (id 가중치가 가장 높습니다.)
- class 선택자 **vs** 특정 요소의 class 선택자 <br/>
  → 특정 요소의 class 선택자 우선!
  ex) .title 보다 h1.title 이 더 구체적임 (구체성의 원칙 적용)
- 같은 class 선택자에 대한 css, 같은 요소 선택자에 대한 css

  ```css
  p {
    color: red;
  }

  p {
    color: green;
  }
  ```

  → 순서상 나중이 우선 (후자 원의 원칙 적용), green으로 값이 적용됩니다.

- 우선순위가 같다면 개수가 많은 CSS가 우선순위가 높습니다.
  <img width="800" src="https://github.com/wanted-pre-onboarding-team-9/Frontend-Interview-Study/assets/74637336/8332bb56-01f3-488d-95d9-f9d4694a85a4"/> <br/>
  → class 하나에 달린 CSS보다 class 두 개에 달린 CSS 우선 순위가 더 높습니다.
  <br/>

## 주의할 점

- !important를 고려하기 전에 명시도를 활용할 방법을 찾아보기. `!important` 사용은 **나쁜 습관**이고 스타일시트 내 자연스러운 종속을 깨뜨려 디버깅을 더 어렵게 만들기에 피해야 합니다. (!important와 inline style은 실무에서 사용을 제한하는 경우가 많다고 합니다.) <br/>
  -> 외부 CSS(Bootstrap 또는 Normalize.css 같은 외부 라이브러리에서)를 재정의하는 페이지 전용 CSS에만 `!important`를 사용합시다.
  <br/>

## 추가 피드백

- 실무에서 어떤 선택자를 사용하는게 좋을까?
  실제로 3~6순위를 많이 사용하는데 항상 순위가 낮은 것부터 사용하고 예외사항을 적용하고 싶을 때 한 단계 위의 우선순위를 적용한다고 생각하면 됩니다. 이렇게 했을 때 가장 꼬이지 않고 CSS 코드를 설계할 수 있게 됩니다.(만약 반대로 처음부터 id selector만 적용하고 그다음에 class선택자를 적용하고 그다음에 tag선택자를 적용하는 방향으로 개발을 한다면 매우 힘든 개발 경험이 될 확률이 높아집니다.)
- id 선택자 vs class 선택자
  실무에서 협업을 위해 class는 디자인 영역에서, id는 개발영역에서 사용한다고 합니다.  
   class와 id의 기능상 구분도 존재하기는 하겠지만, 사실상 기능상의 구분은 무의미하며, 실제 업무 영역에서의 분업 문제로 이러한 개발 방식을 채택하였다고 생각하면 될 것 같다고 합니다.
  <br/>

## 참고

https://velog.io/@ewaterbin/02.-CSS-Selector<br/>
https://developer.mozilla.org/ko/docs/Web/CSS/Specificity<br/>
https://www.zerocho.com/category/CSS/post/588cb95ca63e64132496a5d5<br/>
https://parkgaebung.tistory.com/72<br/>
https://codingapple.com/forums/topic/id-class-%EC%84%A0%ED%83%9D%EC%9E%90%EC%97%90-%EB%8C%80%ED%95%9C-%EC%A7%88%EB%AC%B8/<br/>
https://cocoder16.tistory.com/19<br/>
