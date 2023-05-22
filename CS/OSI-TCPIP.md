# OSI 7계층과 TCP/IP 4계층을 비교하여 설명해주세요.

OSI 7계층과 TCP/IP 4계층은 모두 네트워크 프로토콜 스택에서 사용되는 계층화된 모델

    프로토콜: 네트워크 통신을 위해 미리 정해놓은 공통된 메뉴얼

![image](https://github.com/wanted-pre-onboarding-team-9/Frontend-Interview-Study/assets/111125577/dd47e671-0b93-43a4-8596-0e2badf0604d)

- OSI는 네트워크 시스템 구성을 위한 범용적이고 개념적인 모델
- TCP/IP는 session layer와 presentation layer를 통합하여application layer에 포함되어 있으며, 현재 인터넷에서 사용되는 표준
- 각 layer를 거치는 encapsulation, decapsulation을 반복하며 통신이 이루어짐

**OSI 7 layer**

- application layer: 어플리케이션 목적에 맞는 통신 방법을 제공
  - http, dns, smtp, ftp
- presentation layer: 어플리케이션 간의 통신에서 메시지 포맷 관리
  - 인코딩 ↔ 디코딩
  - 암호화 ↔ 복호화
  - 압축 ↔ 압축 풀기
- session layer: 어플리케이션 간의 통신에서 세션을 관리
  - RPC (remote procedure call)
- transport layer: 어플리케이션 간의 통신 담당. 목적지 어플리케이션으로 데이터 전송
  - tcp: 데이터들이 유실되지않고 올바른 순서로 전송되는 것을 보장 / udp: 필수 기능만 제공
- network layer: 호스트 간의 통신 담당. (ip) 목적지 호스트로 데이터 전송. 네트워크 간의 최적의 경로 결정
- data link layer: 직접 연결된 노드 간의 통신 담당
  - MAC 주소 기반 통신 (ARP)
- physical layer: bits 단위로 데이터 통신

**TCP/IP 4 layer (updated model)**

- application layer: 사용자 애플리케이션과 직접 상호작용
  - 암호화, 압축, 인코딩, 디코딩, 통신회선 구축
- transport layer: 네트워크 종단(end point) 시스템 간의 데이터를 일관성 있고 투명한 데이터 전송을 제공할 수 있도록 두 종단간(end to end)에 오류 복구와 흐름 제어를 제공
  - 운영체제 커널에 구현되어있음
- network layer: IP 주소 할당 및 라우팅을 담당하여 패킷의 전송을 관리
  - 운영체제의 커널에 소프트웨어적으로 구현되어있음
- data link layer:
  - 하드웨어에 구현되어있음 (LAN 카드)
- physical layer: 물리적으로 연결된 두 대의 컴퓨터가 0과 1의 나열을 주고받을 수 있게 해주는 모듈
  - 하드웨어에 구현되어있음

## References

https://velog.io/@amuse/OSI-7-Layers
