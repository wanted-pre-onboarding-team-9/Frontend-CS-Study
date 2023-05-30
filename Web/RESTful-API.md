# RESTful API에 대해 설명해주세요

### REST

- **REST란** Representational State Transfer(표현 상태 전이)의 약어로, 자원을 이름으로 구분해 해당 자원의 상태를 주고받는 모든 것을 의미한다. 어떤 자원에 대해 CRUD 연산을 수행하기 위해 URI(Resource)로 GET, POST 등의 Method를 사용하여 요청을 보내며, 요청을 위한 자원은 특정한 형태로 표현된다.

  ```
  💡 URI란? (feat. URL)
  Uniform Resource Identifier로 인터넷 상의 자원을 식별하기 위한 문자열의 구성을 뜻함.
  URL은 Uniform Resource Locator로 인터넷 상 자원의 위치를 의미하기 때문에 URI는 URL의 개념을 포함함.
  ```

- **REST의 특징**
  1. Server-Client
     - 자원이 있는 쪽이 Server, 자원을 요청하는 쪽이 Client
  2. Stateless
     - 서버가 클라이언트의 상태를 저장하지 않는 무상태(Stateless) 통신 방식
     - 각 API 서버는 Client 요청만을 단순 처리하고, 이전 요청이 다음 요청의 처리에 연관되지 않음.
  3. Cacheable
     - 웹 표준 HTTP 프로토콜을 그대로 사용하므로 HTTP의 특징인 캐싱 기능을 적용할 수 있음
  4. Layered System
     - Client는 REST API Server만 호출함. Client는 Server와 직접 통신하는지, 중간 서버와 통신하는지 알 수 없음.
     - REST Server는 보안, 로드 밸런싱, 암호화 등을 위한 계층이 추가된 다중 계층으로 구성될 수 있으며 Proxy, Gateway와 같은 네트워크 기반의 중간매체를 사용할 수 있음.
  5. Uniform Interface
     - URI로 지정한 Resource에 대한 요청을 통일되고, 한정적으로 수행하는 아키텍쳐 스타일을 의미
     - HTTP 표준 프로토콜을 따르는 모든 플랫폼에서 사용이 가능하며, 특정 언어나 기술에 종속되지 않음.
  6. Self-Descriptiveness
     - 요청 메시지만 보고도 쉽게 이해할 수 있는 자체 표현 구조로 되어있음

### REST API

- **REST API란** REST의 특징을 기반으로 서비스 API를 구현한 것이다.
- **REST API 디자인 가이드**
  1. URI는 정보의 자원을 표현해야 한다.
  2. 자원에 대한 행위는 HTTP Method(GET, POST, PUT, PATCH, DELETE)로 표현한다.
     - 행위(Method)는 URI에 포함하지 않는다.
- **REST API의 설계 규칙**
  - URI는 명사를 사용한다.
    ```
    /getMails // (x)
    /mail; // (o)
    ```
  - 슬래시(/)로 계층 관계를 표현한다.
  - URI 마지막 문자로 슬래시(/)를 포함하지 않는다.
  - 언더바(\_)를 사용하지않고 하이픈(-)을 사용한다
  - URI는 소문자로만 구성한다.
  - HTTP 응답 상태코드를 사용한다.
  - 파일 확장자는 URI에 포함하지 않는다.
    ```
    https://www.naver.com/rest/100/photo.jpg // (x)
    https://www.naver.com/rest/100/photo // (o)
    ```

### RESTful API

- **RESTful API란** REST의 설계 규칙을 최대한 지킨 API다. RESTful API는 네트워크 상에서 클라이언트와 서버 간의 통신을 위한 규칙과 원칙을 제공한다.

## References

https://dev-coco.tistory.com/97
