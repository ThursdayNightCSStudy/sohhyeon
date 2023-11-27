# Array

```js
class Array {
  constructor() {
    this.length = 0;
    this.data = {};
  }

  push(element) {
    this.data[this.length] = element;
    this.length++;
    return this.data;
  }

  pop() {
    const element = this.data[this.length - 1];
    this.length--;
    return this.data;
  }

  insertAt(item, index) {
    for (let i = this.length; i > index; i--) {
      this.data[i] = this.data[i - 1];
    }
    this.data[index] = item;
    this.legnth++;
    return this.data;
  }

  deleteAt(item, index) {
    for (let i = index; i < this.length - 1; i++) {
      this.data[i] = this.data[i + 1];
    }
    delete this.data[this.length - 1];
    this.length--;
    return this.data;
  }
}
```

## 빠른 접근 O(1)

일반적으로 배열의 요소는 하나의 타입으로 통일되어 있으며 서로 연속적으로 인접해있다. 배열의 요소는 동일한 크기를 갖고, 연속적으로 이어져있어 인덱스로 한번에 요소에 접근할 수 있어 O(1)의 시간 복잡도를 가져 매우 효율적이다.

배열의 요소의 메모리 주소는 다음과 같이 할당된다.

```txt
메모리 주소 = 배열의 시작 메모리 주소 + 인덱스 * 요소의 바이트 수
```

예를 들어, 메모리 주소가 1000에서 시작하고 각 요소의 크기가 8byte인 배열이라면, 0번째 인덱스 요소는 1000 + 0\*8 = 1000, 1번째 인덱스 요소의 메모리 주소는 1008, 2번째 인덱스 요소의 메모리 주소는 1016이 된다.

<br>

## 느린 탐색 O(n) : 선형 탐색 (linear search)

정렬되지 않은 배열의 경우, 모든 배열 요소를 처음부터 값을 발견할때까지 선형 탐색해야하므로 (linear search) O(n)의 시간 복잡도를 갖는다.

<br>

## 삽입, 삭제 어려움

배열에 요소를 삽입하거나 삭제하는 경우, 배열 요소를 연속적으로 유지하기 위해 요소를 이동시켜야 한다.

배열의 메소드로는 push, pop, shift, unshift 등이 있다.
push와 pop은 배열 안의 요소들의 이동이 일어나지 않아 속도가 빠르지만, shift와 unshift는 배열의 모든 요소를 한칸씩 앞으로, 뒤로 이동시켜한다.

# 자바스크립트에서의 배열

- 희소 배열(sparse array)
  - 배열의 크기가 정해져있지 않다.
  - 배열의 요소는 동일한 크기를 갖지 않아도 되며, 연속적으로 이어져있지 않을 수도 있다.

사실 자바스크립트에서 배열은 인덱스를 프로퍼티 키로 갖고, length 프로퍼티를 갖는 특수한 객체이다. 자바스크립트에서 사용할 수 있는 모든 값은 객체의 프로퍼티 값이 될 수 있으므로 어떤 타입의 값이라도 배열의 요소가 될 수 있다.

```js
const arr = []; // 빈 배열 생성
arr[0] = 'zero';
arr[20] = 20; // 연속적이지 않으며 서로 다른 자료형을 가진 배열을 만들 수 있다.
```

하지만, 위의 경우처럼 순서와 타입을 고려하지 않고 사용하는 것은 배열의 최적화 기법이 동작하지 않아 이점이 없어진다. 배열은 순서가 있는 자료를 저장하는 용도로 만들어졌기 때문에, 목적에 맞게 사용하는 것이 중요하다.

> ### 참고

- <a href="https://poiemaweb.com/js-array-is-not-arrray">자바스크립트 배열은 배열이 아니다</a>

- <a href="https://ko.javascript.info/array#ref-828">배열</a>
