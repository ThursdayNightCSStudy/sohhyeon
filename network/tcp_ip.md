# TCP (Transfer Control Protocol) IP (Internet Protocol)

TCP란, 두 개의 호스트를 연결하고 데이터 스트림을 교환하게 해주는 네트워크 프로토콜이다. 즉, 한 기기에서 다른 기기로 데이터 전송을 담당한다. IP는 데이터 조각을 최대한 빨리 대상 IP 주소로 보내는 역할을 한다.

즉, IP 주소 체계를 따르고 IP Routing을 이용해 목적지에 도달하면 TCP의 특성을 활용해 송신자와 수신자의 논리적 연결을 생성하고 신뢰성을 유지할 수 있도록 하겠다는 것을 의미한다.

인터넷에서 무언가를 다운로드할때, 중간에 끊기거나 빠지는 부분없이 완벽하게 받을 수 있는 것도 TCP의 특성 덕분이다. 따라서 TCP는 HTTP, HTTPS, FTP, SMTP 등의 프로토콜의 기반이 된다.

# TCP

TCP는 OSI 7계층 중 4계층(Network)에 속한다. 양쪽 단말이 통신할 준비가 되었는지, 데이터가 제대로 전송되었는지, 데이터가 변질되지는 않았는지, 수신자가 잘 받았고, 빠진 부분은 없는지 등을 점검한다. 이런 정보는 TCP 헤더에 담겨있다. TCP 헤더에는 SYNC, ACK, FIN, RST, Source Port, Destination Port, Sequence Number, Window size, Checksum과 같은 신뢰성 보장과 흐름 제어, 혼잡 제어에 관여할 수 있는 요소들도 포함되어있다.

TCP는 포트를 이용해 연결하는데, 이는 단말의 입구를 의미한다. 양쪽 단말이 HTTP 통신할 경우, 80번 포트로 연결해야한다.

<img src="./images/tcp_header.jpg">

<br>

# 3-Way Handshake

<img src="./images/3wayhandshake.png"/>

TCP를 사용해 데이터를 송수신하기 전에 먼저 서로 통신이 가능한지 의사를 묻고 한 번에 얼마나 받을 수 있는지 등의 정보를 확인한다. 이 과정을 통해 송신자와 수신자 간 세션을 수립한다.

> ### step 1 (SYN)

클라이언트는 연결요청 메시지(SYN)를 전송한다. 이때, SYN 플래그 비트는 1이며, 랜덤한 숫자의 Sequence Number x를 함께 전송한다.

> ### step 2 (SYN + ACK)

서버가 SYN(x)를 받고 요청을 수락한다는 신호로 ACK와 SYN 패킷을 보낸다. 이때,Syncrhonize Sequence Number는 y, Acknowledge Number는 x+1로 설정한다.

> ### step 3

클라이언트는 ACK(x+1)과 SYN(y) 패킷을 받고, ACK(y+1)을 서버로 보낸다.
<br><br>

# 4-Way Handshake

3-Way Handshake가 TCP 연결을 초기화할때 사용한다면, 4-Way Handshake는 세션을 종료하기 위한 과정이다.

<img src="./images/FourWayHandshakeProcess.jpg"/>

> ### step 1 (FIN)

서버 또는 클라이언트에서 FIN 패킷을 보내 커넥션의 종료를 요청한다.

> ### step 2 (ACK)

FIN 패킷을 받은 쪽에서 해당 요청을 확인했다는 의미로 ACK 패킷을 전송한다.

> ### step 3 (FIN)

또한 FIN 패킷을 받은 쪽에서 종료 시그널로 FIN 패킷을 전송한다.

> ### step 4 (ACK)

마지막으로 FIN 패킷을 받은 쪽에서 커넥션 종료에 대한 확인으로 ACK 패킷을 전송한다.

<br><br>

## 4단계를 거쳐야 하는 이유

간단히 생각해보면 2,3 단계는 하나로 합쳐서 3-Way Handshake로 세션을 종료할 수 있을 것 같다. 하지만, 각 단계의 상태를 이해하면 그렇게 할 수 없다는 것을 알 수 있다.

2단계에서 서버로부터 ACK 패킷을 전달받았을때, 클라이언트는 서버와의 연결을 종료한다. 하지만, 서버에는 여전히 클라이언트로 전송할 데이터가 남아있을 수 있다. 따라서, 남은 데이터가 있다면 모두 전송한 후에 FIN 패킷을 전송하고, 클라이언트는 ACK 패킷을 전송한다.

만약 4단계에 걸쳐 세션을 종료하지 않는다면, 클라이언트에서 연결 종료를 요청하고 서버로부터 확인 응답을 받았지만, 여전히 전달받은 데이터가 남아있지만, 오프라인 등으로 패킷이 유실되거나 데이터 처리에 예외가 발생한 경우 클라이언트는 세션의 타임아웃이 될때까지 기다려야한다는 문제가 있다.

따라서 4단계에 걸쳐 연결을 종료하는 과정이 필요하다.

<br><br>
reference

- <a hrref="http://www.ktword.co.kr/test/view/view.php?m_temp1=1889">정보통신기술용어해설</a>

- <a href="https://aws-hyoh.tistory.com/entry/TCPIP-%EC%89%BD%EA%B2%8C-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0">네트워크 엔지니어 환영의 기술블로그</a>

- <a href="https://www.geeksforgeeks.org/why-tcp-connect-termination-need-4-way-handshake/">Why TCP Connect Termination Need 4-Way-Handshake?</a>
