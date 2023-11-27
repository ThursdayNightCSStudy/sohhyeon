# Linked List

## 특징

- data와 link
- head와 tail
- 빠른 삽입과 삭제 O(1)
- 느린 검색 O(n)
- 배열보다 2배 이상의 메모리 사용

연결 리스트는 여러 노드들이 연결되어 있는 구조이다. 노드는 data와 link 필드를 갖는다. 노드는 link를 통해 다음 노드에 접근할 수 있다. 연결 리스트에서 맨 앞을 Head, 맨 끝을 Tail이라고 한다.

데이터의 삽입과 삭제의 경우, 앞의 노드와 뒤의 노드를 끊고 다시 연결해주기만 하면 되므로 시간 복잡도는 O(1)이다. 하지만, 배열과 마찬가지로 연결 리스트에서 데이터를 검색할 경우, 순차적으로 확인해야하므로 시간복잡도는 O(n)이 된다.

여러 장점이 있지만, 연결 리스트는 데이터외에도 주소에 대한 정보를 가지고 있기 때문에 배열과 비교하여 2배의 용량이 더 필요하다.

<br>

## 구현

```js
class Node {
  constructor(element) {
    this.element = element; // 데이터
    this.next = null; // 다음 노드를 가리키는 포인터
  }
}

class LinkedList {
  constructor() {
    this.head = null;
    this.size = 0;
  }

  // 리스트의 마지막 요소로 추가
  append(newElement) {
    let newNode = new Node(newElement);
    if (this.isEmpty()) {
      this.head = newNode;
    } else {
      let current = this.head;
      while (current.next) {
        current = current.next;
      }
      current.next = newNode;
    }
    this.size++;
  }

  // 특정 노드 다음으로 추가
  insertAt(newElement, item) {
    let newNode = new Node(newElement);
    let current = this.findNodeBy(item);
    newNode.next = current.next;
    current.next = newNode;
  }

  // 특정 노드 삭제
  remove(item) {
    let preNode = this.findPreviousNodeBy(item);
    preNode.next = preNode.next.next;
  }

  // 특정 노드 조회
  findNodeBy(item) {
    let currentNode = this.head;
    while (currentNode.element !== item) {
      currentNode = currentNode.next;
    }
    return currentNode;
  }
  // 특정 노드 전의 노드 조회
  findPreviousNodeBy(item) {
    let previousNode = this.head;
    while (previousNode.next && previousNode.next.element !== item) {
      previousNode = previousNode.next;
    }
    return previousNode;
  }

  indexOf(item) {
    let currentNode = this.head;
    let index = 0;
    while (currentNode) {
      if (currentNode.element === item) {
        return index;
      }
      index++;
      currentNode = currentNode.next;
    }
    return -1;
  }

  isEmtpy() {
    return this.size === 0;
  }
}
```

> reference

- <a href="https://www.geeksforgeeks.org/implementation-linkedlist-javascript/">Implementation of LinkedList in Javascript
  </a>
