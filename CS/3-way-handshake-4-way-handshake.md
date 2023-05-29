# 3-Way Handshake / 4-Way Handshake

## 이거 먼저..!
> **💡 포트의 상태 정보**
>    - `CLOSED`: 포트가 닫힌 상태
>    - `LISTEN`: 포트가 열린 상태로 연결 요청 대기 중
>    - `SYN_RCV`: SYNC 요청을 받고 상대방의 응답을 기다리는 중
>    - `ESTABLISHED`: 포트 연결 상태
>    - `FIN_WAIT_1`: close()를 진행한 소켓이 진입하는 상태
>    - `FIN_WAIT_2`: `ACK`신호를 받은 `FIN_WAIT_1`소켓이 `FIN_WAIT_2`로변경
>    - `CLOSE_WAIT`: 상대방의 `FIN`을 받은 상태. 상대방 `FIN`에 대한 `ACK`를 보내고 애플리케이션에 종료를 알린다
>    - `TIME_WAIT`: FIN에 대한 ACK를 받고 연결 종료가 완료된 상태. 일정 시간 기다린 후 `CLOSED`로 전이된다.
>    - `LAST_ACK`: `CLOSE-WAIT` 상태를 처리 후 자신의 `FIN`요청을 보낸 후 `FIN`에 대한 `ACK`를 기다리는 상태


>**💡 플래그 정보**
>
>![](https://velog.velcdn.com/images/tkddn_dev8430/post/7723d11d-2657-4c8e-a0c6-d56ae4f3779a/image.jpeg)
>
>  - TCP헤더는 각 1 bit씩 차지하는 6개의 플래그가 있고, 각 플래그는 초기값 0을 가진다.
>  - 패킷은 해당 플래그의 비트를 조절하여 해당 패킷이 어떤 정보를 담고 있는지 알려준다.
>  - `SYN` - Synchronize sequence numbers
  연결 설정, 연결을 위해 랜덤으로 설정하여 세션을 연결하는데 사용. Client와 Server의 Connection을 생성할 때 사용하는 Flag
>  - `ACK` - Acknowledgment
  응답 확인. 응답을 확인했음을 알려준다.
>  - `FIN` - Finish
  연결 해제. Client/Server간 연결을 종료하기 위해 사용. 더 이상 전달할 의미가 없음을 의미한다.

## 👨‍👩‍👦 3-Way Handshake

- TCP 통신을 사용하여 데이터를 전송하기 위해 네트워크 연결을 설정하는 과정
- 양쪽(Client/Server) 모두 데이터를 송/수신하기 위한 준비가 되었음을 보장하고, 시작하기 전에 반대 쪽이 준비되었다는 것을 알 수 있다.
- Client와 Server는 통신 중에 3번의 패킷이 교환되기 때문에, 3-Way Handshake라고 한다.

### 3-Way HandShake의 과정

![](https://velog.velcdn.com/images/tkddn_dev8430/post/82dd2f65-23fe-4d53-a37b-88ec1e8fe852/image.jpeg)

1. **Client는 Server에 접속을 요청하는 SYN을 보낸다.**
    
    Client → `SYN-SENT` / Server → Wait For Client
    
2. **Server는 Client로 부터 SYN을 받고, 요청을 수락하는 ACK와 SYN Flag가 설정된 패킷을 발송한다.**
    
    Client → `SYN-SENT` / Server → `SYN-RECEIVED`
    
3. **Client는 Server에게 ACK보내고, 이후 Client와 Server는 데이터 전송이 가능해진다.**
    
    Client → `ESTABLISHED` / Server → `ESTABLISHED`

<br>

## 👨‍👩‍👧‍👦 4-Way HandShake

- 4-Way HandShake는 연결을 종료하는 과정이다. 여기서 `FIN` 플래그가 사용된다.

![](https://velog.velcdn.com/images/tkddn_dev8430/post/71bee380-239d-4114-854d-73ea7d0f9a7e/image.jpeg)


### 4-Way HandShake의 과정

1. Client가 연결을 끊는다. 이때 서버에 `FIN` 플래그를 보낸다.
    
    Client → `FIN_WAIT_1` / Server → `ESTABLISHED`
    
2. Server는 `FIN` 플래그를 받고, 확인했다는 의미로 `ACK`를 보내고 Client에게 보내고, 서버의 상태를 `CLOSE_WAIT`상태로 변경하고, 미처 보내지 못한 데이터를 마저 보내고, 서버에서 close()를 호출한다.
    
    Client → `FIN_WAIT_2` / Server → `CLOSE_WAIT`
    
3. 데이터를 모두 전송한 후에 Server는 Client의 연결 종료에 합의한다는 의미의 `FIN` 패킷을 Client에게 전달한다. 이때 Client가 확인했다는 `ACK` 패킷을 보내주기 전까지 `LAST_ACK` 상태로 들어간다.
    
    Client → `TIME_WAIT` / Server → `LAST_ACK`
    
4. Client는 확인의 의미로 Server에게 `ACK` 패킷을 보내주고 `CLOSED` 상태로 들어가며, `ACK` 패킷을 전달받은 Server 또한 `CLOSED` 상태로 들어간다.
    
    Client → `CLOSED` / Server → `CLOSED`
    
<br>

## ❓ Question

**3 way handshake 와 4 way handshake에서 단게의 차이가 발생하는 이유**

Client가 종료를 희망해도, Server 쪽에서 전달할 필요가 있는 데이터가 남아있을 경우, Client와 Server의 종료 시점이 다를 수 있다. 그래서 Client에서 `FIN` 패킷을 보냈을 때, Server에서 일단 확인했음을 알려주기 위해 `ACK` 패킷을 전달하고, 이후 Server가 연결 종료를 희망할 때 FIN 패킷을 보내기 때문에 연결할 때와 연결을 종료할 때 단계의 차이가 발생한다.

**초기 Sequence Number인 ISN을 0 부터 시작해서 연속적으로 사용하는 것이 아닌 난수를 생성해서 설정하는 이유는 ?**

연결에 사용되는 포트번호는 유한한 범위 내애서 사용되고, 재사용된다. 따라서 Client와 Server가 과거에 사용한 포트번호는 쌍으로 존재할 가능성이 있다. Server 쪽에서는 연결을 위해 전달받는 `SYN`을 보고 패킷을 구분하는 데 과거에 재사용된 포트번호로 인지할 가능성이 있다. 이런 문제가 발생할 수 있는 가능성을 줄이기 위해 난수로 설정한다.
