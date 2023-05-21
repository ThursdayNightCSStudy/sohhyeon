# HTTP (Hyper Text Transfer Protocol)

인터넷 상에서 클라이언트와 서버가 자원을 주고 받을때 쓰는 통신 규약이다. 클라이언트에서 리소스를 요청하면 서버에서 리소스를 응답한다.

## 무상태성 (Stateless)

HTTP 프로토콜은 요청과 응답을 교환하지만, 이전의 요청, 이전의 응답에 대해서는 관리하지 않는다. 많은 데이터를 빠르고 확실하게 처리하기 위해 간단하게 설계되었기 때문이다.

HTTP의 무상태성을 보완하기 위해 쿠키(Cookie)가 도입되었고, HTTP를 이용한 통신에서도 상태를 관리할 수 있게 되었다.

## URI (Uniform Resource Identifiers)

HTTP는 URI를 사용해서 인터넷 상의 리소스를 지정한다. 서버에 리소스가 지정된 경로를 요청할 수 있다.

## Method

GET, POST, PATCH, PUT, DELETE, HEAD, OPTIONS, TRACE, CONNECT 등의 메소드가 있다.

- HEAD: GET과 같은 기능이지만 메시지 바디는 돌려주지 않는다. URI 유효성과 리소스 갱신 시간을 확인하는 목적으로 사용한다.

- OPTIONS: URI로 지정한 리소스가 제공하고 있는 메소드를 조사하기 위해 사용한다. OPTIONS 메서드로 요청을 보낸 후, 서버에서 제공하는 메소드를 파악한 후 클라이언트에서 해당 메소드로 요청을 보낸다.

- TRACE: WEB 서버에 접속해서 자신에게 통신을 되돌려 받는 루프백(loop-back)을 발생시킨다. 리퀘스트를 보낼때 Max-Forwards 라는 헤더 필드에 수치를 포함시켜 서버를 통과시킬때마다 그 수치를 줄여간다. 수치가 0이 된 곳을 마지막으로 수신한 곳에서 상태코드 200 OK 응답을 되돌려준다. 서버는 응답에 요청받은 메시지를 그대로 반환해주므로 그 안에 로그인에 필요한 정보도 포함되어 있어 문제가 될 수 있다. 크로스 사이트 트레이싱 (XST)과 같은 공격을 일으키는 보안상 문제도 있기 때문에 보통은 사용하지 않는다.

  - XST
    HTTP TRACE 메소드를 이용한 공격 방법으로 이를 통해 HttpOnly 옵션으로 보호된 세션 쿠키를 탈취하는데 사용할 수 있다. 쿠키는 HttpOnly 옵션으로 자바스크립트에서의 쿠키 접근을 제한한다. (ex. document.cookie로의 접근이 제한됨) 하지만, 서비스에 TRACE Method가 허용된 경우 TRACE Method로 웹 요청을 발생시키면, HTTP 요청에는 쿠키가 전달되고, 응답에 쿠키 정보가 포함되어 전달된다.

    - 예를들어 공격자가 XSS 취약점을 바탕으로 공격 코드를 작성해 관리자에게 메일 또는 게시물 작성하면, 관리자가 로그인 상태일때 메일에 포함된 공격링크를 클릭할 경우 웹브라우저는 서버에 TRACE 요청을 보내고 응답에 포함된 인증정보를 확인한 공격자가 세션 쿠키를 탈취하게 된다.

    - TRACE 메소드를 허용하지 않도록 설정할 수 있다.

- CONNECT: 프록시에 터널 접속 확립을 요함으로써 TCP 통신을 터널링 시키기 위해 사용된다. 주로 SSL과 TLS 등의 프로토콜로 암호화된 것을 터널링 시키기 위해서 사용되고 있다.

## 지속 연결

HTTP/1.1과 일부 HTTP/1.0에서는 TCP 연결 문제를 해결하기 위 지속 연결이라는 방법을 고안했다. 지속 연결의 특징은 어느 한쪽이 명시적으로 연결을 종료하지 않는 이상 TCP 연결을 유지한다.

지속 연결을 통해 여러 리퀘스트를 연달아 보낼 수 있는 파이프라인화가 가능하다. 파이프라인화로 인해 응답을 수신할때까지 기다린 후 요청을 보내던 것에서 응답을 기다리지 않고 바로 다음 요청을 보낼 수 있게 되었다. 따라서 여러 요청을 응답을 기다리지 않고 연달아 보내 더 빠르게 응답을 받을 수 있다.

## 비암호화

HTTP를 통해 주고받는 데이터는 평문으로 탈취될 경우, 그대로 노출되는 위험이 있다. 따라서, 정보를 암호화하는 SSL 프로토콜을 사용해 클라이언트와 서버가 자원을 주고받을때 암호화하는 HTTPS를 사용한다.

## wireshark로 실제 패킷 확인하기

- <a href="https://yunzema.tistory.com/358">HTTPS & HTTP의 패킷 평문 노출 여부 Wireshark로 확인</a>
- <a href="https://linuxhint.com/install_wireshark_ubuntu/">How to Install and Use Wireshark on Ubuntu</a>