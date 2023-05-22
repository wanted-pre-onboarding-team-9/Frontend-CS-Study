# Virtual DOM이 무엇인가요?

React가 관리하는 DOM과 유사한 객체로, 이전의 Virtual DOM과 새로운 Virtual DOM을 비교하여 실제 변경된 부분만 DOM에 적용합니다.

브라우저가 서버로부터 HTML 응답을 받아 화면을 그리기 위해 실행하는 과정은 다음과 같습니다.

1. HTML을 파싱해서 DOM을 만든다.
2. CSS를 파싱해서 CSSOM을 만든다.
3. DOM과 CSSOM을 결합해 Render Tree를 만든다.
4. Render Tree와 Viewport의 width를 통해 각 요소들의 위치와 크기를 계산하는 Layout 과정을 거친다.
5. 계산된 정보를 이용해 Render Tree상의 요소들을 실제 Pixel로 그려내는 Paint 단계를 거친다.

위와 같은 과정을 CRP(Critical Rendering Path)라고 하며 특히 4, 5번 과정은 많은 계산을 필요로 하므로 이를 최적화 하기 위해서 Virtual DOM을 사용합니다.
