# Third Party

써드파티란, 사전적으로 제 3자를 말한다. IT 업계에서는 어떤 분야의 원천 기술을 가지고 있는 것이 아니라 원천 기술과 호환되는 상품을 출시하거나 해당 기술을 활용한 파생상품을 생산하는 회사를 말한다. 예를 들어서 게임분야를 보면, 소니나 MS처럼 콘솔 게임기를 개발하면서 게임을 개발하면 퍼스트파티, 게임 하드웨어 제조사의 자회사는 아니지만 투자를 받거나 전략적 제휴 등의 이유로, 출시하는 모든 게임, 혹은 상당수의 게임을 특정 플랫폼의 독점작으로만 개발하면 세컨드 파티, 게임기를 기반으로 게임만 개발하면 써드파티라고 할 수 있다. 프로그래밍에서는 개발을 도와주는 라이브러리, 프레임워크, 플러그인을 만드는 회사를 가리킨다. 

- 프레임워크
  Application 개발 시 필수적인 코드, 알고리즘, 데이터베이스 연동 등과 같은 기능들을 위해 어느정도의 뼈대(구조)를 제공
  (Vue, React, Nest)  

- 라이브러리
  여러 문서를 모아둔 도서관 처럼 특정 기능에 대한 도구/함수들을 모아둔 집합

- 플러그인
  플러그인은 어떤 특정한 하나의 문제를 해결하기 위한 컴포넌트(component)이다. 즉, 사람들이 자주 사용할만한 기능들을 직접 일일이 구현할 필요 없이 필요한 기능들만 그때 그때 찾아서 사용할 수 있도록 미리 만들어 놓은 것이 플러그인이다. 라이브러리보다 조금 더 작은 개념이다. (플러그인의 집합이 라이브러리)

## serverless 
<a href="https://www.serverless.com/">공식문서</a>

- AWS lambda (서버리스 컴퓨팅 플랫폼)를 빌드, 배포를 쉽게 할 수 있도록 해주는 프레임워크
- <a href="https://www.serverless.com/framework/docs-guides-plugins">플러그인</a>을 사용해 필요한 기능을 적용해서 사용가능

```
npm install -g serverless // 설치
sls create --template {template} --path {path} // 프로젝트 생성
sls invoke local -f hello --path lib/data.json // 로컬 람다 호출 
sls invoke -f hello // 원격 람다 호출
sls deploy // 배포
sls remove // 삭제

plugins: // 필요한 기능에 대해 플러그인을 설치하여 yml 파일에 명시
- serverless-esbuild
- serverless-offline 
```

<a href="https://contents.premium.naver.com/3mit/wony/contents/220505105924891hK">3분 IT 써드파티란</a>

