프로세스 동기화란, 병행(concurrent: operating or occurring at the same time) 프로세스들간 공유된 시스템 자원을 효율적으로 사용하는 것을 의미한다. 만족스러운 동기화 매커니즘은 교착상태(deadlocks), 기아상태(starvation)을 방지하는 동시에 동시성(concurrency)를 제공한다.

이러한 프로세스 동기화 방법으로는 세마포어와 뮤텍스가 있다. 각각을 살펴보도록 하자.

# 세마포어 Semaphore

<img src="../images/semaphore.png"/>

세마포어는 여러 프로세스들 간에 공유되는 정수 변수값이다. 이때 사용되는 변수값이 0 또는 1로 고정된 Binary Semaphore와, 여러 프로세스가 공유 자원에 접근할 수 있는 최대 허용치로 설정할 수 있는 Counting Semaphore가 있다. 위의 이미지에서는 Counting Semaphore를 나타내고 있다.

Counting Semaphore에서 semaphore 값은 보통 최대 허용치는 공유 자원에 접근할 수 있는 동시 사용자(스레드, 프로세스)의 수이다. 프로세스가 공유 자원에 접근하면 세마포어는 1씩 감소한다. 세마포어 값이 0이 되면, 그 요청을 한 프로세스는 대기한다. 공유 자원을 다 사용한 프로세스가 있다면, 허용치가 1씩 증가한다.

세마포어는 wait, signal이라는 두 가지 연산을 통해 구현된다.

## Wait Operation

Wait operation은 세마포어 값을 감소시키는 연산이다. 만약 세마포어 값이 0보다 크면 세마포어 값을 감소시키고, 0보다 작거나 같으면 프로세스는 블록된다.

```c
// Semaphore Wait Operation
Function wait(S) is
  if S > 0 then
      // do not block the process
      S ← S - 1;
      return;
  else
      // Block the calling process
    sleep;
  end
end
```

## Signal Operation

Signal operation은 세마포어 값을 증가시키는 연산이다. 만약 대기 중인 프로세스가 있다면, 그 중 하나를 깨운다. 만약 대기 중인 프로세스가 없다면, 세마포어 값을 증가시킨다.

```c
// Semaphore Signal Operation
Function signal(S) is
  if there are processes sleeping on S then
    select a process to wake up;
    wake up the selected process;
    return;
  else
    // no process is waiting
    S ← S + 1;
    return;
  end
end
```

Binary Semaphore에서는 S의 초기값이 1로 설정된다.

```c
procedure P(S)
    while S=0 do wait
    S := S-1   // S를 0로 만들어 다른 프로세스가 들어 오지 못하도록 함
end P

procedure V(S)  // 현재상태는 S가 0임
    S := S+1   // S를 1로 변경
end V
```

> reference

- <a href="https://www.baeldung.com/cs/semaphore">What Is a Semaphore?</a>

- <a hrefe="https://incheol-jung.gitbook.io/docs/q-and-a/computer-science/undefined-1">뮤텍스와 세마포어</a>
