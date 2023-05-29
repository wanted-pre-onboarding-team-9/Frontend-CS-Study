# this 는 몇가지로 추론될수 있는가요? this에 대해 설명해주세요.

자바스크립트에서의 this는 상황에 따라 this가 바라보는 대상이 달라집니다.
this는 기본적으로 실행 컨텍스트가 생성될때 함께 결정됩니다. 실행 컨텍스트는 함수를 호출할때 생성되므로 즉, this는 함수를 호출할때 결정된다고 할 수 있습니다.
this는 크게 4가지로 추론될 수 있으며, 4가지 상황에서의 함수를 호출할때 결정되는 this에 대해 설명하겠습니다.

### 1. 전역 공간에서의 this

전역공간에서 this는 **전역 객체**를 가리킵니다. 브라우저 환경에서 전역객체는 window, node.js 환경에서는 global 입니다.

### 2. 함수 호출시 this

어떤 함수를 함수로서 호출할 경우에는 this가 지정되지 않습니다. 실행 컨텍스트를 활성화할 당시에 this가 지정되지 않은 경우 this는 전역객체를 바라보기 때문에 함수에서의 this는 **전역객체**를 가리킵니다.

### 3. 메서드 호출시 this

어떤 함수를 메서드로서 호출하는 경우 this는 **메서드 앞의 객체**를 가리킵니다.

<img src="https://github.com/wanted-pre-onboarding-team-9/Frontend-Interview-Study/assets/74637336/375bf431-3cf5-4688-baec-5e3b10ab91af"/>

### 4. 생성자 함수 호출시 this

어떤 함수가 생성자 함수로서 호출된 경우 내부에서의 this는 곧 새로 만들 구체적인 **인스턴스** 자신이 됩니다.

### P.S. 명시적으로 this를 바인딩 하는 방법

This에 별도의 대상을 바인딩 하는 방법이 있는데, 명시적으로 this를 바인딩하는 여러가지 방법 중 **화살표 함수**가 있습니다.
화살표 함수는 실행 컨텍스트 생성 시 this를 바인딩하는 과정이 제외됐습니다.
즉, 화살표 함수에서는 접근하고자 하면 스코프체인상 가장 가까운 this에 접근하게 됩니다.
이렇게 화살표 함수를 사용할 경우 별도의 변수로 this를 우회하거나 call/ apply/ bind를 적용할 필요가 없어 더욱 간결하고 편리합니다.

**this 명시적 바인딩 하기 전**
<img src="https://github.com/wanted-pre-onboarding-team-9/Frontend-Interview-Study/assets/74637336/401c415b-d58b-47a7-8099-930b0a796442"/>

**this 명시적 바인딩 하고난 후**
<img src="https://github.com/wanted-pre-onboarding-team-9/Frontend-Interview-Study/assets/74637336/247337d9-54e8-4d63-bb1a-5bbcfcb19cf5"/>

## 참고

코어 자바스크립트 - 정재남 지음, 위키북스 <br/>
https://poiemaweb.com/js-this
