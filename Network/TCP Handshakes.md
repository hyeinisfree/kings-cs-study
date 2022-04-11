# TCP Handshakes

## 3-way handshake

![CleanShot 2022-04-11 at 17.41.21@2x.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/10897de8-d548-404b-8608-bd88383097d9/CleanShot_2022-04-11_at_17.41.212x.png)

- TCP 프로토콜에서 데이터 수신 측과 송신 측이 connection(session이라고도 한다)을 수립하는 과정이다.
- connection을 수립해야지만 수신 측과 송신 측은 데이터를 주고 받을 수 있는 상태가 된다.
- 3-way handshake는 다음과 같은 단계로 이루어진다.
    1. 송신 측은 연결 요청을 담은 패킷을 수신 측으로 보낸다.
    2. 수신 측은 연결 요청을 잘 받았으며, 해당 요청을 수락한다는 의미를 담은 패킷을 송신측으로 보낸다.
    3. 송신 측은 connection이 수립되었음을 수신 측에 알린다.
- 이 과정에서 송신 측과 수신 측은 데이터 송, 수신에 필요한 여러 정보를 주고 받는다.
    - Sequence number
        - TCP는 데이터가 너무 클 경우 여러 조각으로 분할하여 전송하게 된다.
        - 이렇게 잘린 조각들이 순차적으로 수신 측에 도착한다는 보장이 없으므로 송신 측은 해당 데이터가 몇 번째 조각인지 수신 측에 알려줘야한다. (그래야 다시 데이터를 원상복구할 수 있겠지)
        - 송신 측에게 해당 조각이 몇 번째(실질적으로는 몇 번째 바이트)인지 알려주기 위한 것이 헤더의 sequence number이다.
        - 이 sequence number는 1에서부터 시작하는 것이 아니라 랜덤한 숫자로 시작한다. 그래서 이 랜덤한 숫자가 무엇인지 connection을 맺는 과정에서 알려주어야하는 것이다.
    - Window size
        - 흐름 제어를 위해서 송신 측은 수신 측의 버퍼 크기가 몇인지 미리 알고 있어야한다.

## 4-way handshake

![CleanShot 2022-04-11 at 17.41.05@2x.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/1e9cc0b2-e194-4073-bd69-616aefd4c120/CleanShot_2022-04-11_at_17.41.052x.png)

- 3-way handshake를 통해 수립되었던 connection을 종료해야 정상적으로 데이터 송, 수신이 완료가 된다.
- 수신 측, 송신 측 상관 없이 connection을 끊을 수 있다.
- 4-way handshake는 다음과 같은 단계로 이루어진다.
    1. 연결을 종료하고자 하는 요청자가 FIN 패킷을 상대방에게 보낸다.
    2. 요청자로부터 FIN 패킷을 받은 수신자는 ACK 패킷을 요청자에게 보낸다.
    3. 수신자는 자신의 데이터 처리가 모두 끝났다면 요청자에게 FIN 패킷을 보낸다.
    4. 요청자는 connection 종료를 의미하는 ACK 패킷을 보낸다.
