## HTTP?

 **HTTP**는 Hyper Text Transfer Protocol의 줄임말으로써 서버와 클라이언트간에 데이터를 주고 받는 프로토콜. HTTP는 텍스트, 이미지,영상, JSON 등등 거의 **모든 형태의 데이터**를 전송(HTML을 전송하기 위한 통신 규약으로 등장 ) HTTP는 1997년 만들어진 HTTP/1.1가 가장 보편화 되어있으며, 현재는 HTTP/2를 거쳐 HTTP/3까지 개발된 상태입니다. 

 HTTP 통신은 클라이언트와 서버간의 통신에 있어서 별다른 보안 조치가 없기때문에 만약 누군가 네트워크 신호를 가로챈다면 HTTP의 내용은 그대로 외부에 노출됩니다.이런 보안적 문제를 해결하기 위해 등장한 것이 **HTTPS**입니다.

### [HTTPS?](https://devjem.tistory.com/3#HTTPS%-F)

<img width="1000" alt="https적용 화면" src="https://user-images.githubusercontent.com/46683113/172116853-3acc1514-0003-44aa-a6b9-70406aab1600.png">


**HTTPS**가 적용되었다는걸 알려주는게 바로 저 자물쇠 입니다. HTTPS가 옛날부터 보편화되어있지는 않았습니다. 처음에는 **전자상거래** 등 고객의 중요 정보를 다루는 사이트 위주로 사용되었습니다. 그러다가 2014년 구글에서는 HTTP를 HTTPS로 변환하라고 권고하기 시작합니다. 구글은 HTTPS를 적용하는 사이트들에게 **SEO(검색 엔진 최적화)**에 있어서 가산점을 주겠다고 합니다. 사용자 정보의 안전성도 보장받고, 사용자들의 웹사이트 유입도 늘릴수 있으니 HTTPS로 변환할 이유는 충분했을겁니다. 이는 구글 투명성 보고서로 지속적으로 관리하고 있습니다. 

기존의 HTTP 프로토콜은 **전송계층의 TCP**위에서 동작합니다. 여기서 **SSL**(Secure Sockets Layer)이라는 보안계층이 전송계층 위에 올라갑니다. HTTPS는 SSL 위에 HTTP를 얹어서 보안이 보장된 통신을 하는 프로토콜입니다. 이 통신 방식을 **SSL 암호화 통신** 이라고도 합니다. SSL 암호화 통신은 **공개키 암호화 방식**이라는 알고리즘을 통해 구현됩니다.

- cf > TLS
    
    SSL은 원래 Netscape에 의해 개발되었으며 1995년 SSL 2.0 (1.0은 대중에게 공개되지 않음)을 통해 처음으로 등장했습니다. 몇가지 취약점이 발견된후 1996년에 버전 2.0이 SSL 3.0으로 빠르게 대체되었습니다. 참고로 버전 2.0 및 3.0은 때로 SSLv2 및 SSLv3으로 표기됩니다. TLS는 1999년에 새 버전의 SSL으로서 도입되었으며 SSL 3.0을 기반으로 했습니다.
    

![http+ssl](https://user-images.githubusercontent.com/46683113/172117012-b94e00a7-52c6-41d5-9ad7-3100071977a2.png)


### 공개키 암호화 방식

![https://images.velog.io/images/jemni/post/ce853d68-b5e7-4a3b-a8fe-6e6f05ba5aec/%ED%99%94%EB%A9%B4%20%EC%BA%A1%EC%B2%98%202021-10-15%20030143.png](https://images.velog.io/images/jemni/post/ce853d68-b5e7-4a3b-a8fe-6e6f05ba5aec/%ED%99%94%EB%A9%B4%20%EC%BA%A1%EC%B2%98%202021-10-15%20030143.png)

 공개키 암호화 방식에는 **공개키와 개인키** 두 종류의 키가 존재합니다.한쪽 키로 데이터를 암호화 했다면 오직 다른쪽 키로만 복호화를 할 수 있습니다. 개인키는 보통 서버를 운영하는 회사가 가지고 공개키는 CA(Certificate Authority)라는 인증받은 기업들에서 관리합니다.

 단 모든 데이터를 이러한 방식으로 주고 받을 경우 성능의 문제가 생기므로 주고받을 데이터는 대칭키 방식으로 암호화 하고 이 대칭키는 공개키 방식으로 암호화 해서 성능의 문제와 보안의 문제를 둘다 해결합니다. 

- 흐름
    1. 클라이언트가 서버에 접속한다. 이 단계를 Client Hello라고 한다. 이 단계에서는 주고 받는 정보는 아래와 같다
        - **클라이언트 측에서 생성한 랜덤 데이터**: 아래 3번 과정 참조
        - 클라이언트가 지원하는 암호화 방식들 : 클라이언트와 서버가 지원하는 암호화 방식이 서로 다를수 있기 때문에 상호간에 어떤 암호화 방식을 사용할 것인지에 대한 협상을 해야한다. 이 협상을 위해서 클라이언트 측에서는 자신이 사용할 수 있는 암호화 방식을 전송한다.
        - 세션 아이디 : 이미 SSL 헨드쉐이킹을 했다면 비용과 시간을 절약하기 위해서 기존 세션을 재활용하게 되는데 이때 사용할 연결에 대한 식별자를 서버측에 전송한다.
    2. 서버는 Client Hello에 대한 응답으로 Server Hello를 하게 된다. 이 단계에서 주로받는 정보는 아래와 같다.
        - **서버 측에서 생성한 랜덤 데이터** : 아래 3번 과정 참조
        - 서버가 선택한 클라이언트 암호화 방식 : 클라이언트가 전달한 암호화 방식 중에 서버 쪽에서도 사용할 수 있는 암호화 방식을 선택해서 클라이언트에게 전달한다. 이로써 암호화 방식에 대한 협상이 종료되고 서버와 클라이언트는 암호화 방식을 이용해서 정보를 교환한다.
        - 인증서
    3. 클라이언트는 서버의 인증서가 CA에 의해 발급된것인지 확인하기 위해서 클라이언트 (브라우저)에 내장된 CA리스트를 확인한다. CA 리스트에 인증서가 없다면 사용자에게 경고 메시지를 출력한다. 인증서가 CA에 의해서 발급된 것인지를 확인하기 위해서 클라이언트에 내장된 CA의 공개키를 이용해서 복호화한다. **복호화에 성공했다면 인증서는 CA개인키로 암호화된 문서임을 암시적으로 보징된 것이다.** 인증서를 전송한 서버를 믿을 수 있게 된것이다.
        - 클라이언트는 상기 2번을 통해서 받은 서버의 랜덤 데이터와 클라이언트가 생성한 랜덤 데이터를 조합해서 `Pre-Master secret`이라는 키를 생성한다. 이 키는 뒤에서 살펴볼 세션 단계에서 데이터를 주로 받을 때 암호화 하기 위해서 사용할것이다. **이 때 사용할 암호화 기법은 대칭키이기 때문에 `Pre-Master secret` 값은 제 3자에게 절대로 노출 되어서는 안된다.**
        - `Pre-Master secret` 값을 서버로 전송할 때 공개키 방식으로 전달한다. 서버의 공개키로 `Pre-Master secret` 값을 암호화해서 서버로 전송하면 서버는 자신이 비공개키로 안전하게 복호화 할 수 있다. 이때 서버의 공개키는 서버로 받은 인증서 안에 들어 있다. 이 서버의 공개키를 이용해서 `Pre-Master secret` 값을 암호화한 후에 서버로 전송하면 안전하게 전송될 수 있다.
    4. 서버는 클라이언트가 전송한 `Pre-Master secret` 값을 자신의 비공개키로 복호화한다. 이로서 서버와 클라이언트가 모두 `Pre-Master secret` 값을 공유하게 되었다. 그리고 서버와 클라이언트 모두 인련의 과정을 거쳐 `Pre-Master secret` 값을 `Master secret` 값으로 만든다. 이 값은 `session key`를 생성하는데 이 값을 이용해서 서버와 클라이언트는 데이터 대칭키 방식으로 암호화한 후 에 주고 받는다 이렇게 해서 세션키를 클라이언트와 서버가 모두 공유하게 되었다.

#추가 - google

-구글 투명성 보고서 

[Google Transparency Report](https://transparencyreport.google.com/https/certificates?hl=ko-kr&cert_search_auth=&cert_search_cert=&cert_search=include_subdomains:false;domain:www.naver.com&lu=cert_search)

<img width="1000" alt="1" src="https://user-images.githubusercontent.com/46683113/172117126-288919a2-f7dc-4e48-88af-3aeb9726ab88.png">

<img width="1000" alt="2" src="https://user-images.githubusercontent.com/46683113/172117232-453d754c-1e44-4871-9c2d-0261bfa9797a.png">

<img width="1000" alt="3" src="https://user-images.githubusercontent.com/46683113/172117297-421d2e80-27fe-464d-b6ca-cacda0e1e833.png">

<img width="1000" alt="4" src="https://user-images.githubusercontent.com/46683113/172117585-350b7340-c62d-404c-a12d-179aa83983ea.png">

---

출처 : [https://cheese10yun.github.io/https/#null](https://cheese10yun.github.io/https/#null)