# Stack

- 한 방향으로만 데이터를 저장할 수 있는 선형 자료구조이다.

- 스택은 LIFO(Last In First Out, 후입선출)의 자료구조이다. 즉, 나중에 들어간 데이터가 먼저 나오는 자료구조이다.

- 자바스크립트에서 배열의 push와 pop 메소드를 이용하여 스택으로 사용하거나, 별도의 클래스를 만들어서 스택을 구현할 수 있다.

- 데이터 삽입과 삭제는 O(1), 조회 및 검색은 O(n)의 시간 복잡도를 가진다.

```js
// 배열을 이용한 스택 구현
class Stack {
  constructor() {
    this.items = [];
    this.index = 0;
  }

  push(item) {
    this.items.push(item);
    this.index++;
    return this.idex;
  }

  pop() {
    if (this.index === 0) {
      return;
    }
    this.items.pop();
    this.index--;
    return this.index;
  }

  peek() {
    return this.items[this.index];
  }

  isEmpty() {
    return this.index === 0;
  }
}

// 연결리스트를 이용하여 스택 구현
class Node {
  constructor(data) {
    this.data = data;
    this.next = null;
  }
}
class Stack {
  constructor() {
    this.top = null;
  }

  push(data) {
    const newNode = new Node(data);
    newNode.next = this.top;
    this.top = newNode;
  }

  pop() {
    if (this.isEmpty()) return null;
    const popNode = this.top;
    this.top = this.top.next;
    return popNode.data;
  }

  peek() {
    if (this.isEmpty()) return null;
    return this.top.data;
  }

  isEmpty() {
    return this.top === null;
  }
}
```

# Queue

- 스택과 마찬가지로 한 방향으로만 데이터를 저장할 수 있는 선형 자료구조이다.

- 스택은 FIFO(First In First Out, 선입선출)의 자료구조이다. 즉, 먼저 들어간 데이터가 먼저 나오는 자료구조이다.

- 큐는 순서대로 처리해야하는 작업을 임시로 저장해두는 용도로 많이 사용된다.

- 자바스크립트 엔진에서 비동기 함수 실행시 콜백들이 대기열로 들어오는 Task Queue가 대표적 예이다.

- 자바스크립트 배열에서 push, shift 메소드를 이용하여 큐로 사용하거나, 별도의 클래스를 만들어서 큐를 구현할 수 있다.

- 데이터 삽입과 삭제는 O(1), 조회 및 검색은 O(n)의 시간 복잡도를 가진다.

```js
// 배열을 이용한 큐 구현
export class Queue {
  constructor() {
    this.items = [];
  }

  enqueue(item) {
    this.items.push(item);
  }

  // 배열의 shift 메소드를 사용하게 되면, 배열의 0번째 요소를 삭제하고 기존 요소들을 앞으로 당겨줘야하므로 시간복잡도가 O(n)이 된다. (QUEUE는 원래 O(1)의 시간복잡도를 갖는다.)
  dequeue(item) {
    return this.items.shift();
  }

  peek() {
    return this.items[0];
  }

  isEmpty() {
    return this.items.length === 0;
  }

  size() {
    return this.items.length;
  }
}

// 연결리스트를 이용하여 큐 구현
class Node {
  constructor(data) {
    this.data = data;
    this.next = null;
  }
}

class Queue {
  constructor() {
    this.front = null;
    this.rear = null;
    this.size = 0;
  }

  isEmpty() {
    return this.size === 0;
  }

  enqueue(data) {
    const newNode = new Node(data);
    if (this.isEmpty()) {
      this.front = newNode;
      this.rear = newNode;
    } else {
      this.rear.next = newNode;
      this.rear = newNode;
    }
    this.size++;
  }

  dequeue() {
    if (this.isEmpty()) return null;
    const popNode = this.front;
    this.front = this.front.next;
    this.size--;
    return popNode.data;
  }
}
```
