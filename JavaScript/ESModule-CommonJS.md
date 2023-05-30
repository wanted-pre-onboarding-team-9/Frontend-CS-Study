# ESModule과 CommonJS의 작동방식 차이, 빌드 결과물 차이에 대해 설명해주세요.

ESModule과 CommonJS는 JavaScript 모듈 시스템의 두 가지 주요한 형식입니다.

### 작동방식

**ESModule**

ESModule은 ECMAScript 2015(ES6)에서 도입된 표준 모듈 시스템입니다. ESModule은 정적인 모듈 시스템으로, 코드를 실행하기 전에 모듈의 의존성을 분석하고 모듈을 로드합니다.

1. `import`**/**`export`문을 사용하여 모듈을 가져옵니다.

   ```jsx
   // add.js
   export function add(x, y) {
     return x + y;
   }

   // main.js
   import { add } from "./add.js";

   add(1, 2);
   ```

2. 모듈 파일이 실행되기 전에 모듈의 의존성을 분석합니다. 정적인 구조로 모듈끼리 의존하도록 강제하기 위해 import path에 동적인 값을 사용할 수 없고, export는 항상 최상위 스코프에서만 사용할 수 있습니다.

   ```jsx
   import util from `./utils/${utilName}.js`; // 불가능

   import { add } from "./utils/math.js"; // 가능

   function foo() {
     export const value = "foo"; // 불가능
   }

   export const value = "foo"; // 가능
   ```

3. 정적 분석을 통해 빌드 단계에서 모듈 간의 의존 관계를 파악할 수 있습니다. 의존성 그래프를 통해 필요한 모듈들을 로드하고 실행합니다.
4. 모듈은 한 번만 로드되며, 내보내기된 값들이 단일 인스턴스로 공유됩니다.
5. [top-level await](https://nodejs.org/api/esm.html#top-level-await)를 지원하기 때문에 비동기적으로 동작합니다.

**CommonJS**

CommonJS는 Node.js환경에서 자바스크립트 모듈을 사용하기 위해 만들어진 모듈 시스템입니다. CommonJS는 동기적으로 동작하며, 모듈이 필요한 시점에 로드합니다.

1. `require`**/**`module.exports`를 사용하여 모듈을 가져옵니다.

   ```jsx
   // add.js
   module.exports.add = (x, y) => x + y;

   // main.js
   const { add } = require("./add");

   add(1, 2);
   ```

2. `require`/`module.exports` 를 동적으로 할 수 있습니다. 따라서 빌드 타임에 정적 분석을 적용하기 어렵고, 런타임에서만 모듈 관계를 파악할 수 있습니다.

   ```jsx
   // require
   const utilName = /* 동적인 값 */
   const util = require(`./utils/${utilName}`);

   // module.exports
   function foo() {
     if (/* 동적인 조건 */) {
       module.exports = /* ... */;
     }
   }
   foo();
   ```

3. require 순서에 따라 스크립트를 즉시 실행합니다.
4. 모듈은 여러 번 로드될 수 있으며, 내보내기된 값들은 복사된 새로운 인스턴스로 사용됩니다.
5. top-level await가 불가능하므로 모듈 파일을 동기적으로 로드하고 실행합니다.

### 빌드 결과물

**ESModule**

- ESModule을 빌드할 때는 번들러(예: Webpack, Rollup)가 모듈 그래프를 분석하여 필요한 모듈만 번들에 포함시킵니다. 이 과정에서 번들러는 모듈 간의 의존성을 최적화하고, 중복된 코드를 제거(tree-shaking)하는 것이 쉽게 가능하며 번들의 크기를 줄일 수 있습니다.
- ESModule의 빌드 결과물은 여러 개의 작은 파일로 분리될 수 있으며, 각 파일은 `import` 및 `export` 문으로 명시된 모듈 경계를 유지합니다.
- package.json의 type field가 `module`로 되어있으면 JavaScript 파일이 ESM으로 해석됩니다.

**CommonJS**

- CommonJS는 빌드 시점에 모듈의 의존성을 알 수 없기 때문에 번들러가 모든 의존성을 포함한 번들을 생성하게 됩니다. 따라서 번들의 크기가 더 커지는 단점을 가지고 있습니다.
- 빌드 결과물은 동기적으로 모듈을 로드하기 때문에, 메인스레드가 모듈을 모두 불러오기 전까지 아무것도 할 수 없는 상태(blocking)가 됩니다.
- package.json의 type field 기본값은 `commonjs`이고, 이 때 JavaScript 파일은 CSM으로 해석됩니다.

## References

[CommonJS와 ESM에 모두 대응하는 라이브러리 개발하기: exports field](https://toss.tech/article/commonjs-esm-exports-field)
[[JavaScript] CommonJS, ES Module 이해하기](https://mukma.tistory.com/217)
