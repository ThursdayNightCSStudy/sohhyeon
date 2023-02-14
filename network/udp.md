# UDP (User Datagram Protocol)

UDP는 전송계층(Transport Layer)에 해당하는 프로토콜 중의 하나이다. 다른 프로토콜로는 TCP가 있다.

UDP는 다음과 같은 특징을 갖는다.

- 데이터그램이라는 데이터 단위를 갖는다.
- 비연결형으로 3-way handshake 등의 과정이 없다.
- 속도가 빠르다.
- 일방적으로 데이터를 전송하며 데이터의 정확성을 보장하지 않는다.
- 애플리케이션은 오류, 손실, 중복을 허용할 수 있어야 한다.
- UDP 헤더의 Checksum 필드로 최소한의 오류만 검출한다.
- 신뢰성보다 연속성과 전송 속도가 중요한 실시간 스트리밍, DNS 조회 등에 자주 사용된다.
- 서버와 클라이언트는 1대1, 1대N, N대M으로 연결할 수 있다.

<img src="https://www.cloudflare.com/img/learning/ddos/glossary/user-datagram-protocol-udp/tcp-vs-udp.svg"/>
