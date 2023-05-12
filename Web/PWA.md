## 개요

새로운 기술과 Progressive Enhancement(점진적 향상) 기법을 사용하여 네이티브 앱이 가진 장점을 사용자에게 제공하는 크로스 플랫폼 웹 앱입니다.

### 핵심 요구사항

- 사용자 중심의 성능 최적화에 중점을 두어 빠른 속도를 유지해야 합니다.
- 모든 브라우저에서 작동해야 합니다.
- 모든 화면 크기에서 사용할 수 있어야 합니다.
- 오프라인 페이지를 제공합니다.
- 홈 화면에 설치 혹은 추가할 수 있습니다.

### Web 장점

- 전체 웹에서 검색하고, 쉽게 공유할 수 있습니다.
- 웹 사이트에 방문할 때마다 항상 최신 버전입니다.
- 하나의 코드베이스로 여러 디바이스에서 접근이 가능합니다.
- 패키지화, 추가 컨텐츠 검토, 업데이트 지연이 필요하지 않습니다.

### Platform-specific Apps 장점

- 홈 화면, 독, 작업 표시줄에 표시됩니다.
- 네트워크 연결에 관계없이 동작합니다.
- 로컬 파일 시스템에서 파일을 읽고 쓸 수 있습니다.
- USB, Bluetooth 등을 통해 연결된 하드웨어에 접근할 수 있습니다.
- 연락처, 캘린더 이벤트 같은 데이터와 상호 작용이 가능합니다.

### Progressive Enhancement(점진적 향상)

Progressive Enhancement와 Graceful Degradation(우아한 성능 저하)은 아래의 핵심 사항을 가집니다.

- 모든 코드를 실행할 수 있는 **최신 브라우저**의 사용자에게는 **최상의 환경**을 제공한다.
- 기능이 제한된 이전 브라우저 사용자를 포함하여 가능한 **많은 사용자**에게도 **필수 컨텐츠 및 기능**을 제공한다.

**Progressive Enhancement(점진적 향상)**  
표준 HTML, CSS, JavaScript를 시작으로 모든 곳에서 실행되는 코드를 작성하고, API를 사용할 수 없을 때 적절한 fallback을 통해 레이어를 쌓는 패턴입니다.

**Graceful Degradation(우아한 성능 저하)**  
정반대로 최신 기술을 사용하여 최신 브라우저 사용자를 위한 기능을 구현하는 것에 중점을 두며, 이전 브라우저에서도 비슷하게 작동되도록 구현합니다.

두 가지 방식은 모두 효과적이고, 서로 보완이 가능합니다.

<br>

## Service Workers

PWA의 기본적인 부분으로, 네트워크에 관계없이 빠른 로딩과 오프라인 접근, 푸시 알림 등의 기능을 제공합니다.

worker context에서 실행되기 때문에 DOM에 접근할 수 없고, 메인 JavaScript와 다른 스레드에서 동작하므로 연산을 가로막지 않습니다. 또한 네트워크 요청을 수정할 수 있다는 점에서 공격에 취약하기 때문에 보안 상의 이유로 HTTPS에서만 동작합니다.

![](https://velog.velcdn.com/images/hadam/post/ce9cc056-a3c3-451e-a11e-a5f549f465df/image.png)

사용자가 Service Worker에 포함된 리소스를 요청하면 네트워크 프록시처럼 동작하며 요청을 가로챕니다. 이후 일반적인 일처럼 Cache Storage API 또는 네트워크에서 리소스를 제공해야 하는지, 로컬 알고리즘에서 리소스를 생성해야 하는지 결정할 수 있습니다.

### 등록

```js
const register = async () => {
  if ("serviceWorker" in navigator) {
    const registration = await navigator.serviceWorker.register("/serviceworker.js");
  }
};

const unregister = async () => {
  if ("serviceWorker" in navigator) {
    const registration = await navigator.serviceWorker.getRegistration();
    if (registration) {
      await registration.unregister();
    }
  }
};
```

**등록 여부 확인**

1. 개발자 도구를 엽니다.
2. Application 탭으로 이동합니다.
3. Service Workers를 선택합니다.
4. script URL이 activated 상태로 표시되는지 확인합니다.

### 범위

Service Worker가 위치한 폴더에 따라 결정됩니다.
예를 들어 `example.com/my-pwa/sw.js`에 있다면, `example.com/my-pwa/demos/`처럼 `my-pwa` 경로와 그 이하의 모든 경로를 제어할 수 있습니다.

범위당 Service Worker는 하나만 허용됩니다.

> PWA와 관련된 모든 요청을 가로챌 수 있도록 root에 최대한 가깝게 설정하는 것이 가장 일반적입니다.

### Lifecycle

**❶ install**

- `install` 이벤트는 Service Worker가 실행되는 즉시 트리거됩니다.
- 클라이언트를 제어하기 전에 필요한 모든 항목을 캐시할 수 있는 단계입니다.
- `event.waitUntil()`에 전달한 Promise를 통해 설치 성공 여부를 나타냅니다. Promise가 reject되면 설치에 실패했다는 신호가 나타나며, 브라우저는 Service Worker를 삭제합니다.

  ```js
  self.addEventListener("install", (event) => {
    console.log("V1 installing...");

    // cache a cat SVG
    event.waitUntil(caches.open("static-v1").then((cache) => cache.add("/cat.svg")));
  });
  ```

**❷ waiting**

- Service Worker가 업데이트되어 기존 Service Worker가 존재하는 경우, 브라우저가 Service Worker를 한 번에 하나만 실행하도록 보장하기 위해 기존 Service Worker가 더 이상 클라이언트를 제어하지 못할 때까지 활성화를 지연합니다.
  - 수동으로 업데이트하려면 `register` 콜백 함수에 인자인 `registration`의 `update()` 메소드를 호출합니다.
- 기존 Service Worker가 제어하는 웹페이지를 닫을 때까지 기다리지 않고, 활성화된 Service Worker를 제거하여 설치가 완료되는 즉시 활성화하려면 `install` event 핸들러에서 `self.skipWaiting()`을 호출합니다.

**❸ activate**

- 기존 Service Worker가 존재하지 않았을 경우,
  - Service Worker가 클라이언트를 제어하고 push, sync와 같은 기능 이벤트를 다룰 준비가 됐을 때 발생합니다.
  - 페이지를 새로고침하기 전까지는 클라이언트를 제어할 수 없습니다.
  - `clients.claim()`을 호출하여 클라이언트를 제어할 수 있습니다.
  ```js
  self.addEventListener("activate", (event) => {
    clients.claim();
    console.log("V1 now ready to handle fetches!");
  });
  ```
- 이전 Service Worker가 사라지고, 새 Service Worker가 클라이언트를 제어할 수 있게 되면 발생합니다.
  - 데이터베이스 마이그레이션이나 캐시 삭제와 같은 작업을 수행하기 이상적인 시기입니다.
  - `install`과 동일하게 `event.waitUntil()`을 사용할 수 있습니다.
  ```js
  self.addEventListener("activate", (event) => {
    // delete any caches that aren't in expectedCaches
    // which will get rid of static-v1
    event.waitUntil(
      caches
        .keys()
        .then((keys) =>
          Promise.all(
            keys.map((key) => {
              if (!expectedCaches.includes(key)) {
                return caches.delete(key);
              }
            })
          )
        )
        .then(() => {
          console.log("V2 now ready to handle fetches!");
        })
    );
  });
  ```

1. installing
   `install` 이벤트가 발생했지만 아직 완료되지 않았습니다.
2. installed
   설치 완료 상태입니다. 다만, 기존 Service Worker가 제어하는 웹페이지가 켜져 있을 경우 대기 상태가 계속 유지됩니다. 웹페이지를 닫을 때까지 기다리지 않고 설치가 완료되는 즉시 활성화하려면 `install` 이벤트 핸들러 내에서 `self.skipWaiting`을 호출합니다.
3. activating
   `activate` 이벤트가 발생했지만 아직 완료되지 않았습니다.
   페이지 새로고침 전까지는 클라이언트를 제어할 수 없습니다.
   `self.clients.claim()`을 호출하면 클라이언트 제어가 가능합니다.
4. activated
   fetch, sync, push 등 기능 이벤트 제어가 가능합니다.
5. redundant
   설치에 실패했거나 새로운 Service Worker로 교체되었을 때 곧 소멸될 상태를 의미합니다.

<br>

## Caching

### Caches

브라우저는 서로 다른 정책에 따라 리소스를 캐시하고 제공할 수도 있고, 아닐 수도 있습니다. 따라서 이러한 정책에 의존하는 것이 아닌, 클라이언트 측 스토리지를 사용하여 보다 효과적으로 제어할 수 있습니다.

- **Web storage**
  - localStorage와 sessionStorage를 포함합니다.
  - 단순 key/value 문자열 쌍을 저장합니다.
  - 제한적이고 동기식 API를 사용합니다.
    <br>
- **IndexedDB**
  - 객체 기반 데이터베이스(NoSQL)입니다.
  - 비동기 API를 사용합니다.
  - 많은 양의 구조화된 데이터를 저장하는데 적합합니다.
    <br>
- **Cache storage**
  - key/value 데이터 모델입니다.
  - Service Worker가 제공하는 기능 중 하나입니다.
  - 비동기 API를 사용합니다.
  - 네트워크로 불러온 리소스를 저장하는데 적합합니다.

> WebSQL과 ApplicationCache는 deprecated 되었으므로 사용하면 안 됩니다.

### 항목

사용자 인터페이스를 렌더링하는 데 필요한 최소 리소스로 시작할 수 있습니다.

- 메인 페이지 HTML
- 메인 유저 인터페이스에 필요한 CSS, JavaScript, 이미지
- 기본 경험을 렌더링하는 데 필요한 JSON 파일과 같은 데이터
- 웹 폰트 등

### API 사용

**assets 다운로드 및 저장**  
`open` 메서드의 첫 번째 인자로 캐시 이름에 해당하는 문자열을 전달하여 캐시를 새로 생성하거나, 이미 만들어진 캐시를 가져올 수 있습니다. Cache 객체를 resolve하는 Promise가 반환됩니다.

```js
const cache = await caches.open("pwa-assets");
```

`add`, `addAll` 메서드를 이용해 리소스를 캐싱합니다.

```js
const cache = await caches.open("pwa-assets");
cache.add("styles.css");
cache.addAll(["/styles.css", "/app.js"]);
```

**Service Worker에서의 캐싱**  
가장 일반적인 시나리오 중 하나는 `install` 이벤트 핸들러 내부에서 캐시하는 것입니다. Service Worker의 스레드는 언제든지 중지될 수 있으므로, `waitUntil` 메서드에 `add` 혹은 `addAll` Promise가 완료될 때까지 기다리도록 요청하여 모든 assets을 저장하고 앱을 일관성있게 유지할 수 있습니다.

```js
const urlsToCache = ["/", "app.js", "styles.css", "logo.svg"];
self.addEventListener("install", (event) => {
  event.waitUntil(async () => {
    const cache = await caches.open("pwa-assets");
    return cache.addAll(urlsToCache);
  });
});
```

**캐시된 response 가져오기**  
`match` 메서드 인자에 HTTP request or URL을 전달하여 response 객체를 resolve하는 Promise를 받을 수 있습니다.

```js
// Global search on all caches in the current origin
caches.match(urlOrRequest).then(response => {
   console.log(response ? response : "It's not in the cache");
});

// Cache-specific search
caches.open("pwa-assets").then(cache => {
  cache.match(urlOrRequest).then(response) {
    console.log(response ? response : "It's not in the cache");
  }
});
```

### 캐싱 전략

가장 일반적인 전략은 다음과 같습니다.

- **Cache First**  
  캐시된 response를 먼저 검색하고, 없을 경우 네트워크에 요청을 전달합니다.

- **Network First**  
  네트워크에 먼저 요청을 전달하고, response가 반환되지 않으면 캐시를 확인합니다.

- **Stale While Revalidate**  
  캐시에서 response를 처리하는 동안, 백그라운드에서 최신 버전을 요청하고 다음에 asset이 요청되었을 때 캐시에 저장합니다.

- **Network-Only**  
  항상 네트워크에 요청합니다. 캐시는 참조되지 않습니다.

- **Cache-Only**  
  항상 캐시에서 응답합니다. 네트워크는 참조되지 않습니다. 이 전략을 사용하여 제공될 assets은 요청되기 전 캐시에 추가되어 있어야 합니다.

<br>

**Cache First**

<img src="https://velog.velcdn.com/images/hadam/post/cec57a97-b687-4bbc-9332-acc1db9a7794/image.png" />

`fetch` 이벤트를 통해 네트워크 요청을 인터셉트할 수 있습니다. Service Worker에게 요청이 들어오면 캐시를 검색한 뒤 존재한다면 캐시된 response를, 찾을 수 없다면 요청을 네트워크로 전달합니다.

```js
self.addEventListener("fetch", (event) => {
  event.respondWith(
    caches.match(event.request).then((cachedResponse) => {
      // It can update the cache to serve updated content on the next request
      return cachedResponse || fetch(event.request);
    })
  );
});
```

그 외의 전략은 [링크](https://web.dev/learn/pwa/serving/#network-first)를 참고해 주시기 바랍니다.

<br>

## 설치

### Web App Manifest

공식 확장자는 `.webmanifest`이지만, `application/manifest+json`이나 `text/json`과 같은 JSON 컨텐츠 타입이면 작동하기 때문에 많은 PWA가 `manifest.json`을 사용하고 있습니다.

1. **추가**  
   `app.webmanifest` 파일을 root folder에 만듭니다.

   ```js
   {
       "name": "My First Application"
   }
   ```

2. **연결**  
   포함된 모든 HTML에 `link` element를 이용하여 연결합니다.

   ```html
   <html lang="en">
     <title>This is my first PWA</title>
     <link rel="manifest" href="/app.webmanifest" />
   </html>
   ```

3. **작성**  
   다음과 같은 많은 구성요소들이 존재합니다.
   - name
   - short_name
   - icons
   - start_url
   - display
     그 외의 추가 구성요소들은 [MDN](https://developer.mozilla.org/en-US/docs/Web/Manifest)에서 확인할 수 있습니다.

### `beforeinstallprompt` event

브라우저마다 설치 버튼이 다르게 제공되기 때문에, 일관된 사용자 경험을 제공하기 위해서는 자신만의 설치 환경을 구현하는 것이 좋습니다.

브라우저가 설치 가능하다는 것을 감지하면 `beforeinstallprompt` 이벤트를 실행합니다. 따라서 다음과 같이 구현할 수 있습니다.

1. `beforeinstallprompt` event listener를 추가합니다.
2. `event`를 저장해 둡니다. (추후 필요)
3. 원하는 UI를 표시합니다.
4. 커스텀 설치 버튼이 클릭되면 저장해둔 `event`의 `prompt` 메서드를 호출하여 브라우저의 프로세스를 거치도록 합니다.

```js
// This variable will save the event for later use.
let deferredPrompt;
window.addEventListener("beforeinstallprompt", (e) => {
  // Prevents the default mini-infobar or install dialog from appearing on mobile
  e.preventDefault();
  // Save the event because you'll need to trigger it later.
  deferredPrompt = e;
  // Show your customized install prompt for your PWA
  // Your own UI doesn't have to be a single element, you
  // can have buttons in different locations, or wait to prompt
  // as part of a critical journey.
  showInAppInstallPromotion();
});
```

## 참고 자료

- [Learn PWA - web.dev](https://web.dev/learn/pwa)
- [The service worker lifecycle](https://web.dev/service-worker-lifecycle/)
- [Progressive Enhancement](https://developer.mozilla.org/en-US/docs/Glossary/Progressive_Enhancement)
