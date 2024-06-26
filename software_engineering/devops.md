# DevOps (Development Operations)

DevOps는 2009년 처음 등장한 단어로 소프트웨어 개발과 운영을 통합하여 효율성, 협력, 속도, 안정성을 개선하는 <b>개발 및 운영 방법론</b>이다. 전통적으로 개발팀과 IT 운영팀은 분리되어 각자의 역할을 수행했지만 DevOps는 이러한 경계를 허물고 개발팀과 운영팀 사이의 협력과 커뮤니케이션을 강화한다. DevOps의 방법론으로는 스크럼(Scrum), 칸반(Kanban), 애자일(Agile) 등이 있으며, 이러한 방법론은 개발과 운영의 협업과 효율성을 향상시키는 데 도움을 준다.

## 역할

1. 소프트웨어 개발부터 배포, 운영, 모니터링까지의 전체 생명주기를 관리하며, 개발과 운영 간의 협업을 강화하여 릴리즈 주기를 단축하고 문제를 신속히 해결할 수 있도록 돕는다다. 이를 통해 조직은 고객에게 더 빠르고 안정적인 제품 및 서비스를 제공할 수 있다.

2. 개발팀(Dev)과 IT 운영 팀(Ops) 간 원활하고 지속적인 커뮤니케이션, 협업, 통합, 가시성 및 투명성을 장려한다. 

3. 자동화, 표준화, 모니터링 등의 원칙을 적용하여 개발과 운영의 효율성을 높이고 신속한 제품 개선을 가능하게 한다.

## 툴

DevOps(데브옵스)사례를 따르는 사람들은 종종 DevOps “툴체인”의 일부로 DevOps 친화적인 툴을 사용한다. 이러한 툴의 목표는 소프트웨어 전송 워크플로(또는 "파이프라인")의 다양한 단계를 추가로 간소화하고, 단축하고, 자동화하는 것이다. 다음은 다양한 DevOps(데브옵스) 라이프사이클 단계에서 사용되는 툴의 예시이다.

- 계획: 이 단계는 비즈니스 가치 및 요구사항을 정의하는 데 도움이 된다. 샘플 툴로는 알려진 문제를 추적하고 프로젝트 관리 및 유지하는 데 도움이 되는 Jira 또는 Git가 있다.
- 코딩: 이 단계에는 소프트웨어 설계 및 소프트웨어 코드 생성이 포함된다. 샘플 툴로는 GitHub, GitLab, Bitbucket 또는 Stash가 있다.
- 구축: 이 단계에서는 소프트웨어 빌드 및 버전을 관리하고 자동화된 툴을 사용하여 코드를 컴파일하고 패키징하여 향후 제품 릴리즈에 제공한다. 소스 코드 저장소 또는 패키지 저장소를 사용한다. 이러한 저장소는 제품 릴리즈에 필요한 "패키지" 인프라 역할도 한다. 샘플 툴로는 Docker, Ansible, Puppet, Chef, Gradle, Maven 또는 JFrog Artifactory가 있다.
- 테스트:  이 단계에서는 최적의 코드 품질을 보장하기 위해 지속적인 테스트(수동 또는 자동)를 수행한다. 샘플 툴로는 JUnit, Codeception, Selenium, Vagrant, TestNG 또는 BlazeMeter가 있다.
- 배포: 이 단계에는 제품 릴리즈를 운영 단계로 관리, 조정, 예약 및 자동화하는 데 도움이 되는 툴이 포함될 수 있다. 샘플 툴로는 Puppet, Chef, Ansible, Jenkins, Kubernetes, OpenShift, OpenStack, Docker 또는 Jira가 있다.
- 운영: 이 단계에서는 운영 중인 소프트웨어를 관리한다. 샘플 툴로는 Anabilities, Puppet, PowerShell, Chef, Salt 또는 Otter가 있다.
- 모니터링: 이 단계에서는 운영 환경의 특정 소프트웨어 릴리즈에서 발생하는 문제에 대한 정보를 식별하고 수집한다. 샘플 툴로는 New Relic, Datadog, Grafana, Wireshark, Splunk, Nagios 또는 Slack이 있다.

## 사례

DevOps(데브옵스)사례는 지속적인 개선 및 자동화 개념을 반영한다. 많은 사례가 하나 이상의 개발 주기 단계에 중점을 둔다. 이러한 사례는 다음과 같다.

- 지속적인 개발. 이 사례는 DevOps 라이프사이클의 계획 및 코딩 단계에 걸쳐 적용된다. 버전 제어 메커니즘이 관련될 수 있다.
- 지속적인 테스트. 이 사례는 애플리케이션 코드를 작성하거나 업데이트하는 동안 자동화되고 사전 예약된 지속적인 코드 테스트를 포함한다. 이러한 테스트를 수행하면 코드를 더 빠르게 운영 환경에 제공할 수 있다.
- 지속적인 통합(CI). 이 사례는 구성 관리(CM) 툴을 다른 테스트 및 개발 툴과 함께 사용하여 개발 중인 코드의 운영 준비 상태를 추적한다. 테스트와 개발 간의 신속한 피드백을 통해 코드 문제를 신속하게 파악하고 해결하는 작업이 포함된다.
- 지속적인 제공. 이 사례는 테스트 후 사전 운영 또는 스테이징 환경으로 코드 변경을 제공하는 작업을 자동화한다. (코드 변경 사항이 정기적으로 빌드 및 테스트되어 리포지토리에 통합되는 과정을 통해 계속 품질을 유지하면서 개발을 진행)
- 지속적인 구축(CD). 지속적인 제공과 마찬가지로 이 사례는 신규 또는 변경된 코드를 운영 단계로 자동 릴리즈한다. 지속적인 구축을 수행하는 회사에서는 코드 또는 기능 변경을 하루에 여러 번 릴리즈할 수 있다. Docker, Kubernetes 및 기타 컨테이너 기술을 사용하면 서로 다른 구축 플랫폼 및 환경에서 코드의 일관성을 유지하여 지속적인 구축을 지원할 수 있다.
- 지속적인 모니터링. 이 사례는 작동 중인 코드와 이를 지원하는 기본 인프라에 대한 지속적인 모니터링과 관련된다. 피드백 루프를 통해 버그 또는 문제를 보고한 후 다시 개발 단계로 되돌아갑니다.
- 코드형 인프라. 이 사례는 다양한 DevOps 단계에서 소프트웨어 릴리즈에 필요한 인프라 프로비저닝을 자동화하는 데 사용될 수 있다. 개발자는 기존 개발 툴 내에서 인프라 "코드"를 추가한다. 예를 들어 개발자는 Docker, Kubernetes 또는 OpenShift에서 필요에 따라 스토리지 볼륨을 생성할 수 있다. 또한 운영 팀은 이 사례를 통해 환경 구성을 모니터링하고, 변경 사항을 추적하며, 구성 롤백을 간소화할 수 있다.

### 참고

<a href="https://github.com/ThursdayNightCSStudy/sohhyeon.git">Devops란</a>