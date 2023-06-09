## JavaScript 최적화 방법에 대해서 설명해주세요.

1. 코드 최소화: 불필요한 공백, 주석, 줄바꿈을 최소화 하여 파일 자체의 크기를 줄임으로서 JS 파일을 로드하는 시간을 줄일 수 있습니다.
2. 캐싱 사용: **브라우저 캐시**에 JS 파일을 저장하여 다시 재방문한 경우 캐싱되어 있는 파일은 다시 다운로드하지 않도록 합니다.
3. 비동기 로드: 파일이 큰 JS 파일이 다운로드 되는 경우 **비동기적**으로 처리하여 다운로드 동안 화면 **랜더링이 끊기지 않도록** 하여 웹 사용성을 향상시킬 수 있습니다.
4. 루프, 조건문 최소화: 반복 횟수를 줄이거나 알고리즘 자체를 개선하여 성능을 향상 시킬 수 있습니다. 
5. Lazy Loading: 각 JS 파일이 필요한 경우에만 로드하여 웹 사이트 초기 로드 시간을 줄여 사용성을 향상시킬  수 있습니다.

그 외에 웹 서비스에 따라 여러 기술이 있을 수 있습니다.
