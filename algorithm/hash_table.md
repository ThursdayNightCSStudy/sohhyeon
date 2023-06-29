# hash table

해시 테이블은 해시 함수를 통해 생성된 해시를 키로 갖고, 해시와 맵핑된 데이터가 저장되는 자료구조이다. 자바스크립트에서는 Map과 Object(객체의 경우, 키의 데이터타입은 문자열로 제한됨)이 해시 테이블 자료구조에 해당된다. (파이썬의 경우, Dictionary, Java와 Go,Scala는 Map, Ruby는 Hash)
해시 테이블은 데이터를 삽입, 삭제, 조회 시 모두 O(1) 시간복잡도를 가지므로 매우 빠른 속도로 자주 사용된다. 하지만 실제 시간복잡도는 해시 함수의 성능에 달려있다. 해시 함수가 얼마나 빠른지, 그리고 얼마나 고르게 데이터를 분배해서 충돌의 확률을 줄이는지.

해시 테이블의 구성 요소는 키, 해시함수, 해시, 값 4가지로 구성된다.

- 키
  고유한 값으로 해시 함수의 입력값이다.

- 해시 함수
  키를 해시로 바꿔주는 역할을 한다. 해시를 키로 변환하는 것은 불가능하므로 단방향 함수이다. 서로 다른 키가 동일한 해시로 생성되는 경우를 해시 충돌이라고 하는데, 해시 충돌은 일으키는 확률을 최대한 줄이는 함수를 만드는 것이 중요하다.

- 해시
  해시 함수의 출력값이다. 저장소에 키로 사용된다.

- 값
  저장소에 최종적으로 저장되는 값으로 해시값을 사용해 저장, 조회, 삭제, 검색할 수 있다.

## 해시 테이블 구현

```js
class HashTable {
  constructor(size = 53) {
    // 해시 테이블의 size 매개변수 값이 없을 경우, 기본값으로 53을 설정한다. (테이블의 길이가 소수이면 충돌이 더 적어진다고 한다.)
    this.keyMap = new Array(size);
  }

  private hash(key) {
    let total = 0;
    const PRIME = 31;
    for (let i = 0; i < Math.min(key.length, 100); i++) {
      // 키로 입력받은 값의 최대 100번째 글자까지 반복하도록 제한을 두고
      const char = key[i];
      const value = char.charCodeAt(0) - 96; // char(문자 한 글자)의 UTF-16 코드 값을 구해서 96을 빼준다. (소문자 a는 97부터 시작)
      total = (total * PRIME + value) % this.keyMap.length; // 생성한 keyMap 배열보다 커지면 안되므로 keyMap의 길이로 나눠 나머지를 구한다
    }
  }

  set(key, value) { // 해시 충돌이 발생할 수도 있으므로 separate chaining 개별 체이닝을 활용해 set, get 메서드를 구현해보자
    const index = this.hash(key);
    if(!this.keyMap[index]) {
      this.keyMap[index] = [];
    }

    this.keyMap[index].push([key, value])
  }

  get(key) {
    const index = this.hash(key);
    if(this.keyMap[index]) {
      for(let i=0; i<this.keyMap[index].length; i++) {
        if(this.keyMap[index][i][0] === key) {
          return this.keyMap[index][i][1];
        }
      }
    }
    return;
  }

  keys() {
    const keysArr = [];
    for(let i=0; i< this.keyMap.length; i++) {
      if(this.keyMap[i]) {
        for(let j=0; j<this.keyMap[i].length; j++) {
          if(!keyArr.includes(this.keyMap[i][j][0])) {
            keysArr.push(this.keyMap[i][j][0]);
          }
        }
      }
    }
    return keysArr;
  }

  values() {
     const keysArr = [];
    for(let i=0; i< this.keyMap.length; i++) {
      if(this.keyMap[i]) {
        for(let j=0; j<this.keyMap[i].length; j++) {
          if(!keyArr.includes(this.keyMap[i][j][1])) {
            keysArr.push(this.keyMap[i][j][1]);
          }
        }
      }
    }
    return keysArr;
  }
}
```
