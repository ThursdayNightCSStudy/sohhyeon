# System Call

시스템 호출은 운영 체제의 커널이 제공하는 서비스에 대해 응용 프로그램의 요청에 따라 커널에 접근하기 위한 인터페이스이다.

시스템 콜에는 각 번호가 할당되고, 각 시스템 콜은 시스템 콜 핸들러 함수 주소로 구성되는 시스템 콜 테이블이 있다. 운영체제는 주소에 저장되어 있는 기능을 수행한다. 작업이 완료되면 CPU에게 인터럽트를 발생시켜 수행이 완료되었음을 알린다.

## 사용하는 이유

<img src="../images/mode.png"/>

운영체제 내부에서는 컴퓨터가 CPU를 어떻게 사용하느냐에 따라 두 가지 방식으로 컴퓨터를 제어한다. 유저모드는 CPU의 명령어를 마음대로 설정할 수 없다. 커널모드에서는 CPU를 직접 컨트롤 할 수 있다. 프로세스는 실행되는 과정에서 수없이 유저모드와 커널모드를 왔다갔다 한다. 두 모드 간의 스위칭은 시스템 콜을 통해 이루어진다. 현재 운영체제가 유저모드를 사용하고 있을때, 사용자 입력에 의해 시스템 콜이 호출이 되면 커널모드로 바뀐다. 사용자 요청에 맞는 작업을 하고 다시 유저모드로 돌아온다. 평소에는 유저모드로 대기하고 있다. 

운영체제에서 두 가지 모드로 구분하는 이유는 자원을 보호하기 위함이다. 누구나 쉽게 CPU 자원에 접근하고 조작할 수 있다면 시스템 전체를 망가뜨릴 수도 있을 것이다. 따라서 이러한 명령어들은 특별하게 커널 모드에서만 실행할 수 있도록 설계되었고, 만약 유저 모드에서 시스템 콜을 호출할 경우에는 운영체제에서 불법적인 접근이라 여기고 인터럽트를 발생시킨다.

- 유저모드
  - 유저 어플리케이션 코드 실행

- 커널모드
  - 모든 자원(드라이버, 메모리, CPU 등)에 접근, 명령 가능

## 시스템 콜 유형

- 프로세스 컨트롤
  - 프로세스 생성 및 종료
  - 메모리에 로드, 실행
  - 프로세스 속성 값 확인, 지정
  - wait 이벤트, signal 이벤트
  - 메모리 할당 

- 파일 매니지먼트
  - 파일 생성, 파일 삭제
  - 열기, 닫기
  - 읽기, 쓰기, Reposition
  - 파일 속성 값 확인, 지정

- 디바이스 매니지먼트
  - 디바이스 요청 및 해제
  - 읽기, 쓰기, Reposition
  - 디바이스 속성 확인, 지정
  - 비물리적 디바이스 해제 및 장착

- 정보 관리
  - 시간 확인, 시간 지정
  - 시스템 데이터 확인, 지정
  - 프로세스, 파일, 디바이스 속성 조회 및 설정

- 통신
  - 메시지 송,수신
  - 상태 정보 전달
  - remote 디바이스 해제 및 장착 

- 보안
  - permission 설정 및 획득

## 예시 

```java
cp in.txt out.txt // in.txt 내용을 복사해서 out.txt 파일을 만들어라
```
다음은 위의 명령어를 실행했을때, 시스템 콜이 동작하는 과정이다.

<img src="../images/system_call_example.png"/>


## fork, wait, exec

### fork

fork는 프로세스를 생성할때 사용한다.

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

int main(int argc, char *argv[]) {
    printf("pid : %d", (int) getpid()); 
    
    int rc = fork();				
    
    if (rc < 0) {
        exit(1);
    }								
    else if (rc == 0) {				
        printf("child (pid : %d)", (int) getpid());
    }
    else {							
        printf("parent of %d (pid : %d)", rc, (int)getpid());
    }
}
```

### wait

부모 프로세스가 자식 프로세스의 종료를 대기해야 하는 경우 사용

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/wait.h>

int main(int argc, char *argv[]) {
    printf("pid : %d", (int) getpid()); 
    
    int rc = fork();				
    
    if (rc < 0) {
        exit(1);
    }									
    else if (rc == 0) {					
        printf("child (pid : %d)", (int) getpid());
    }
    else {								
        int wc = wait(NULL)				
        printf("parent of %d (wc : %d / pid : %d)", wc, rc, (int)getpid());
    }
}
```

### exec

fork는 자신의 복사본을 생성하여 실행하는 반면, exec는 자신의 복사본이 아닌 다른 프로그램을 실행해야 할 경우에 사용

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/wait.h>

int main(int argc, char *argv[]) {
    printf("pid : %d", (int) getpid()); 
    
    int rc = fork();					
    
    if (rc < 0) {
        exit(1);
    }								
    else if (rc == 0) {				
        printf("child (pid : %d)", (int) getpid());
        char *myargs[3];
        myargs[0] = strdup("wc");		
        myargs[1] = strdup("p3.c");	
        myargs[2] = NULL;				
        execvp(myarges[0], myargs);		
        printf("this shouldn't print out") /
    }
    else {								
        int wc = wait(NULL)			
        printf("parent of %d (wc : %d / pid : %d)", wc, rc, (int)getpid());
    }
}
```

> reference
- <a href="https://coduking.com/entry/%EC%9A%B4%EC%98%81%EC%B2%B4%EC%A0%9C-%EC%9C%A0%EC%A0%80%EB%AA%A8%EB%93%9C-%EC%BB%A4%EB%84%90%EB%AA%A8%EB%93%9C-%EC%8B%9C%EC%8A%A4%ED%85%9C%EC%BD%9C">운영체제: 유저모드, 커널모드, 시스템콜</a>