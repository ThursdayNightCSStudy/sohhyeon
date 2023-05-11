# Trie

- 트라이는 문자열을 검색해 저장된 문자열 중 일치하는 문자열이 있는지 확인하는데 주로 사용되는 특별한 종류의 트리다. 문자열 저장을 위해 공간을 많이 쓰지만, 탐색에 효율적이다.

- 트라이는 루트에 노드를 저장하고, 노드는 child와 endOfWord를 갖는다.

- children은 hash map, array, linked list로 구현할 수 있다. 아래의 구현 방식은 해시 맵을 사용한 방법으로 글자를 키로 갖고, 노드를 벨류로 갖는다.

- endOfWord 플래그는 단어의 끝을 나타내고, true인 모든 문자열을 찾아 자동완성을 구현할때 사용된다. 예를 들어, 'hello', 'hell', 'hi', 'hellium'이 저장되어있고 'he'를 입력했을때, 자동완성을 구현하려면, he의의 자식을 탐색하면서 endOfWord가 true인 'hello', 'hell', 'hellium'을 모두 찾아내면 된다.

- Trieㅇ자동완성의 시간 복잡도는 O(n)으로, 이때 n은 노드의 개수이다.

```js
class Node {
  constructor() {
    this.children = {};
    this.endOfWord = false;
  }
}

class Trie {
  constructor() {
    this.root = new Node();
  }

  insert(word) {
    let current = this.root; // 시작은 루트부터

    for (let i = 0; i < word.length; i++) {
      const currentChar = word.charAt(i);
      let node = current.children[currentChar];

      if (!node) {
        node = new Node();
        current.children[currentChar] = node;
      }

      current = node;
    }
    current.endOfWord = true;
  }

  search(word) {
    let current = this.root; // 시작은 루트부터

    for (let i = 0; i < word.length; i++) {
      const currentChar = word.charAt(i);
      let node = current.children[currentChar];

      if (!node) {
        return false;
      }

      current = node;
    }
    return current.endOfWord;
  }

  autoComplete(word) {
    let current = this.root; // 시작은 루트부터

    const answer = [];
    for (let i = 0; i < word.length; i++) {
      const currentChar = word.charAt(i);
      let node = current.children[currentChar];

      if (!node) {
        return answer; // 자동완성으로 검색할 문자열로 시작하는 단어가 없는 경우
      }

      current = node;
    }

    this.helper(
      word[word.length - 1],
      current,
      answer,
      word.substring(0, word.length - 1)
    );

    return answer;
  }

  helper(currentChar, current, answer, prefix) {
    console.log(currentChar, current, answer, prefix);

    if (current.endOfWord) {
      answer.push(prefix + currentChar);
    }
    for (let c of Object.keys(current.children)) {
      this.helper(c, current.children[c], answer, prefix + currentChar);
    }
  }
}

/**
 * const trie = new Trie();
 * trie.insert('hell');
 * trie.insert('hellium');
 * trie.insert('hello');
 *
 * trie.autoComplete; ('hel'); //['hell', 'hellium', 'hello']
 */
```
