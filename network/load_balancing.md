# Load Balancing

둘 이상의 CPU 혹은 저장장치와 같은 컴퓨터 자원에 작업을 여러대의 서버, 컴퓨터 혹은 다른 자원으로 나누어 분배하는 컴퓨터 네트워크 기술이다. 클라이언트의 요청 트래픽을 제어함으로써 애플리케이션의 가용성, 확장성, 보안 및 성능이 향상된다.

## 로드 밸런싱 알고리즘

### Round Robin

> 라운드 로빈은 요청을 모든 사용가능한 리소스에 균등하게 분배한다. 각 새로운 요청은 순서에 따라 다음 리소스에 할당된다. 예를 들어 서버가 3개인 경우, 첫번째 요청은 서버 1로, 두 번째 요청은 서버 2로, 세 번째 요청은 서버 3으로, 그리고 다시 4번째 요청은 서버 1로 분배된다.

<br>

### Least connection

> 최소 연결은 요청이 이루어진 시점에 활성화된 연결 수가 가장 적은 리소스로 요청을 라우팅한다. 이렇게 하면 리소스가 고르게 활용되고 한 리소스에 과부하가 걸리는 것을 방지할 수 있다.

<br>

### IP Hash

> IP 해시는 클라이언트의 IP 주소를 기반으로 서버에 요청을 할당한다. 따라서 동일한 클라이언트의 요청은 항상 동일한 서버로 전달되어 서버 지속성을 유지하는데 유용하다.

<br>

### Weighted Round Robin

> 가중치 라운드 로빈은 라운드 로빈과 유사하지만 각 리소스에 다른 가중치를 할당할 수 있다. 가중치가 높은 리소스는 더 많은 요청을 받고, 가중치가 낮은 리소스는 더 적은 요청을 받는다.

## 서버가 다운된 경우

CPU 사용량 또는 메모리 사용량, 네트워크 트래픽이 일정 수준을 넘어 서버가 다운된 경우에 로드 밸런서는 다음과 같은 단계로 트래픽을 재분배하여 다운타임을 방지하고 원활한 사용자 경험을 보장한다.

- 주기적인 헬스 체크

  로드 밸런서는 여러대의 서버들에 주기적으로 헬스 체크를 실행한다. 헬스 체크란, 요청을 보냈을때 특정 시간 내에 응답이 돌아오는지 확인하는 것을 말한다. 만약, 헬스 체크에 실패하거나 에러를 응답한 경우, 로드 밸런서는 해당 서버를 'unhealthy'로 표시한다.

- 가용 서버 풀에서 제거

  unhealthy 상태의 서버는 가용 서버 풀에서 제거하여 더 이상 트래픽이 해당 서버로 분산되지 않도록 한다. 요청이 들어오면, 가용 서버 풀안에 있는 서버들에만 요청을 분산해서 보냄으로써, 'unhealthy' 상태의 서버 유무와 관계없이 요청이 처리되도록 한다.

- 복구된 서버 다시 풀에 추가

  'unhealthy' 상태의 서버가 복구되면, 로드 밸런서는 헬스 체크를 실행하고, 통과하면 다시 'healthy' 상태로 표시하여 가용 서버 풀에 추가한다.

또한 로드 밸런서는 CPU 사용량, 메모리 사용량, 네트워크 트래픽 등의 특정 메트릭을 기반으로 서버에 장애가 발생할 수 있는 시기를 감지할 수 있다. 이렇게 설정해두면, 기준에 따라 가용 서버 풀에서 해당 서버를 사전에 제거하여 시스템에 미치는 영향을 최소화할 수 있다.

## 유즈케이스

### HTTP-HTTPS

로드 밸런서는 웹사이트를 HTTP에서 HTTPS로 변경하는 과정에서 중요한 역할을 한다. HTTPS는 웹사이트와 사용자 간 전송되는 데이터를 암호화해서 통신하는 프로토콜이다.

HTTP에서 HTTPS로 전환될때 전환이 원활히 이루어지고 사용자 경험에 지장을 주지 않도록 몇 단계를 수행해야 한다.

HTTPS로 전환하기 위해서는 우선 웹 서버에 SSL/TLS 인증서가 설치되어있어야 한다. 웹 서버에 인증서가 설치했다면, 로드밸런서가 HTTPS 트래픽을 처리하도록 구성해야한다.

즉, 로드 밸런서가 SSL/TLS 연결을 종료하도록 구성해야한다. 즉, 들어오는 HTTPS 트래픽을 복호화하여 웹 서버에 일반 HTTP 트래픽으로 전달한다. 그리고 로드 밸런서는 다시 웹 서버의 응답을 암호화하여 클라이언트에 HTTPS 트래픽으로 보낸다. 이 프로세스는 SSL/TLS 종료라고 한다. 로드 밸런서가 클라이언트와 웹 서버 사이에서 <b>프록시 서버</b> 역할을 수행하여 <u>웹 서버 대신 모든 SSL/TLS 암호화 및 복호화를 처리</u>한다.

또한 <u>로드 밸런서로 들어오는 모든 HTTP 트래픽을 HTTPS 트래픽으로 자동 리디렉션</u>하도록 구성하여 사용자가 항상 웹사이트의 보안 버전으로 연결되도록 할 수 있다.

### E-커머스 웹사이트

e-커머스 웹사이트에서 이벤트 등으로 많은 트래픽이 생기는 경우, 사용자 요청에 대한 응답이 느리거나 없을 수 있다. 로드 밸런싱은 들어오는 요청들을 여러대의 웹서버로 분배한다.