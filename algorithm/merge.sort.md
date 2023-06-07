# 병합 정렬

병합 정렬은 각 하위 배열에 하나의 항목이 존재할 때까지 배열을 하위 배열로 나눈다. 그리고 각 하위 배열을 정렬된 순서로 병합한다.

병합 정렬은 이후에 병합할 n개의 배열을 생성해야 하므로 공간 복잡도가 O(n)이라는 단점을 갖지만 시간 복잡도는 O(nlog(n))을 갖는다.

```js
function mergeSort(array) {
  const half = array.length / 2;

  if (array.length < 2) {
    return array;
  }

  const left = array.splice(0, half);
  reutrn merge (mergeSort(left), mergeSort(right))
}

function merge(left, right) {
  let arr = [];

  while(left.length && right.length) {
    if(left[0] < right[0]) {
      arr.push(left.shift())
    } else {
      arr.push(right.shift())
    }
  }

  return [...arr, ...left, ...right]
}
```
