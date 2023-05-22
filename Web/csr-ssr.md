# CSR/SSR

## CSR(Client-Side-Rendering)

CSR은 페이지의 뼈대가 되는 최소한의 HTML만 서버가 랜더링하고 내부 세부 내용은 모두 클라이언트에서 JavaScript를 통해 처리된다.

CSR에서는 데이터 요청, 이벤트 처리, 복잡한 페이지 표현을 모두 JS를 통해서 수행하기 때문에 페이지를 랜더링하기 위한 JS 파일의 크기가 커진다. 그래서 JS의 파일의 사이즈에 따라  FCP와 TTI가 늘어난다.

> - FCP(First Contentful Paint): 페이지가 로드되기 시작하고 컨텐츠의 일부가 랜더링 될 때까지의 시간
> - TTI(Time To Interactive) : JS의 실행이 완료되고, 페이지의 상호작용이 가능하게 될 때까지의 시간

<br />

![Untitled](https://github.com/wanted-pre-onboarding-team-9/Frontend-Interview-Study/assets/49917043/55130565-eb5f-4c96-9d1c-54a16f0b6ef3)


### CSR의 장점

- **자연스러운 사용자 경험**
    
    전체 웹 앱이 첫번째 요청에서 다운로드가 완료된 후에는, 서버에서는 페이지 랜더링이 일어나지 않는다. 그래서 뷰가 변경될 때 별도의 새로고침 없이 페이지를 탐색할 수 있고, 페이지간 라우팅 속도가 빠르기 때문에 사용자에게 자연스러운 사용자 경험을 제공할 수 있다.
    
- **서버와 코드 분리**
    
    서버와 클라이언트의 역할이 다르기 때문에 각 영역에 따라 코드를 구분하고 분리하여 관리할 수 있다.
    

### CSR의 단점

- **검색 최적화(SEO)**
    
    검색 최적화(SEO)는 서버 랜더링에 의해 만들어진 웹을 크롤링하여 컨텐츠를 선정하는데, CSR의 경우 서버는 최소한의 구조만 가지고 있고 콘텐츠가 거의 없기 때문에 검색 최적화 부분에서 취약점을 가지고 있다.
    
- **초기 랜더링**
    
    초기에 서버에서 모든 리소스를 가져오기 때문에, JS 번들 파일이 크거나, 성능에 문제가 있어 초기 랜더링 시간이 길어질 경우 사용자가 에러로 인식할 수도 있다.
    
- **Data Fetching**
    
    데이터를 사용하기 위해 서버와 별도의 통신이 필요하다. 그리고 이때 빈 데이터가 보일 때나, 데이터가 커서 불러오는 시간이 길어질 경우 등, 각 상황에 대한 처리가 클라이언트에서 필요하다.
    
<br />
<br />

## SSR(Server-Side-Rendering)

SSR은 서버가 사용자 페이지 요청을 받아 전체 HTML을 만들어 응답하여 화면을 보여주는 방식이다. 이때 필요한 데이터가 모두 포함되어 전달된다. 서버에서 화면을 구성하는 것과 데이터를 받아오는 것 모두 담당하기 때문에 클라이언트 단에서 렌더링에 필요한 코드가 필요하지 않다.

![11](https://github.com/wanted-pre-onboarding-team-9/Frontend-Interview-Study/assets/49917043/3f28f8a8-6ba4-475c-a07e-6d36def0500e)

### SSR의 장점

- **초기 랜더링이 빠르다**
    
    CSR과 달리 서버에서 데이터 요청, 화면 구성까지 모두 담당하기 때문에 JS 번들의 크기가 작아진다. 결국 처리해야하는 JS의 물리적인 양이 줄어들기 때문에, 화면이 랜더링되고(FCP) 상호작용이 가능하게 되기까지(TTI) 간 사이가 짧아진다. 결국 사용자는 초기 랜더링 시간이 빠르다고 느낀다.
    
- **검색 최적화(SEO)**
    
    SSR로 만들어진 컨텐츠에 대해서 검색엔진 크롤러가 쉽게 크롤링 할 수 있어 검색 최적화 측면에서 이점을 가진다.
    

### SSR의 단점

- **서버의 성능에 영향을 받는다.**
    
    동시에 많은 트래픽이 발생하거나, 네트워크가 느린 경우 서버의 성능이 저하될 수 있어, 페이지를 랜더링하는데 영향을 줄 수 있다.
    
- **전체 페이지가 새로고침된다.(확인)**
    
    서버에서 페이지를 만들어 준 이후에 새로운 서버 데이터가 필요한 경우, 전체 페이지를 새로고침해야 할 수 있다. 
    
<br />
<br />


## 추가 내용

### TTI, TTV

> - TTI - Time To Interact : 사용자가 웹 브라우저에서 컨텐츠를 인터렉션할 수 있는 시점
> - TTV - Time To View : 사용자가 웹 컨텐츠를 볼 수 있게 되는 시점

<br />

![222](https://github.com/wanted-pre-onboarding-team-9/Frontend-Interview-Study/assets/49917043/6b6f4a13-a717-4c00-b10d-b8ade05e7b05)


CSR의 타임라인을 보면 

1. 사이트에 접속하여 서버로 부터 응답을 받는다
2. JS를 다운로드 받는다.
3. React로 만들어진 동적으로 조작 가능한 JS파일을 실행한다.
4. 사용자가 실제 가능한 페이지가 보인다. **( TTV, TTI )**

**→ CSR에서는 사용자가 웹 페이지의 컨텐츠를 볼 수 있는 시점(TTV)와 사용가능한 시점이 같다.**

![3333](https://github.com/wanted-pre-onboarding-team-9/Frontend-Interview-Study/assets/49917043/ab2854a2-3773-4679-9dbb-81f2ba2b9d5f)


SSR의 타임라인을 보면

1. 사이트에 접속하여 서버로 부터 응답을 받는다. 
2. 서버로 부터 전달받은 응답으로 이미 화면 구성이 끝난 웹 페이지를 사용자에게 보여준다. **( TTV )**
3. HTML에 JS 로직을 연결한다
4. 사용자가 페이지를 실제 사용가능하다 **( TTI )** 

**→ SSR에서는 사용자가 웹 페이지의 컨텐츠를 보는 시점과 실제 사용이 가능한 시점이 차이가 있다.**

<br />

### SSG (Static Site Generation)

SSR과 동일하게 서버로부터 완성된 HTML 파일을 받아오지만, SSR과 달리 HTML 파일 생성 시점이 페이지가 빌드 되는 시점이다. 

사용자가 웹페이지를 방문하면, **엣지 캐싱되어있는 HTML 파일**을 클라이언트로 반환해주고, 브라우저는 해당 HTML을 다운로드하여 사이트를 보여준다.

**장점** - 빌드 타임에 HTML 파일이 만들어지기 때문에 빠른 FP, FCP, TTI를 제공한다. 일관성있는 페이지를 보여줄 수 있다.

**단점** - 모든 URL에 대해서 HTML 파일이 필요하다. 따라서 URL을 예측하기 힘들 경우 적용하기 어렵다.

<br />

### SSR과 CSR, SSG는 어떤 페이지에 적합한가?

검색 결과에 노출될 필요가 없고, 사용자와 상호작용이 많아 매끄러운 화면 전환이 필요한 페이지 **→ CSR**  
사용자 유입이 검색 엔진을 통해 이루어지고, 매번 같은 내용을 보여주어야 하는 페이지 **→ SSR**  
페이지의 업데이트가 거의 필요없는 페이지 **→ SSG**  