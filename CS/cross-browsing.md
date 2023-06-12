## 크로스 브라우징

> **크로스 브라우징**  
> 웹 사이트에 접근하는 브라우저의 종류에 상관없이 동등한 화면과 기능을 제공할 수 있도록 만드는 작업

브라우저는 서로 다른 렌더링 엔진을 가지고 있어, 같은 코드라도 다르게 해석하여 최종적으로 다른 화면을 제공합니다. 따라서 크로스 브라우징을 통하여 어느 브라우저를 통해서든 동등한 화면을 제공받을 수 있도록 만들어야 합니다.

이때 '동일한'이 아니라 **'동등한'** 이라는 표현을 사용하는 이유는 모든 브라우저에서 완전히 똑같은 화면을 만드는 것이 아니라, 같은 수준의 정보와 기능을 제공하는 것이 목표이기 때문입니다.

## 크로스 브라우징 워크 플로우

### 1. 초기 기획

어떤 웹 사이트를 만들고 어떤 기능과 디자인으로 할 지 결정한 후, 사이트의 고객을 생각하고 고객이 사용하는 브라우저, 기기 등을 파악하여 그에 맞는 기술을 사용해서 개발할 수 있도록 기획해야 합니다.

### 2. 브라우저 호환성 확인하기

브라우저의 호환성은 [MDN](https://developer.mozilla.org/ko/) 혹은 [Can I Use](https://caniuse.com/) 등의 사이트에서 확인할 수 있습니다.

<img width="826" alt="스크린샷 2023-06-12 오후 11 35 52" src="https://github.com/sena-22/untitled/assets/110877564/0d1ffdf7-fa50-4e76-b633-d91a8e9df37d"> 

<img width="1373" alt="스크린샷 2023-06-12 오후 1 17 28" src="https://github.com/sena-22/untitled/assets/110877564/f888d6be-b5c3-43fa-9f23-e02c50c7e318">

### 3. 테스트 / 발견

- 데스크톱 브라우저(크롬, 엣지, 파이어폭스, 오페라, 사파리) 및 휴대폰, 태블릿 브라우저 등에서 테스트를 진행합니다.

- TestComplete, LambdaTest, BitBa 등의 크로스 브라우징 테스트 툴을 사용할 수 있습니다.

### 4. 수정 / 반복

- 테스트 단계에서 버그가 발견된다면 버그가 발생하는 위치를 특정하고, 그 브라우저에서의 해결 방법을 정한 후 수정합니다.

> 참고  
> [https://poiemaweb.com/css3-vendor-prefix](https://poiemaweb.com/css3-vendor-prefix)