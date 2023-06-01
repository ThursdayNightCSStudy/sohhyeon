# 삽입 정렬

삽입 정렬은 배열을 순차적으로 검색하면서 정렬되지 않은 항목들을 배열의 왼쪽의 정렬된 부분으로 이동시킨다.

시간 복잡도는 이중 반복문을 실행해야 하므로 O(n^2)을 갖는다.

```js
function insertionSort(arr, n) {
  let i, key, j;
  for (i = 1; i < n; i++) {
    key = arr[i];
    j = i - 1;
    while (i >= 0 && arr[j] > key) {
      arr[j + 1] = arr[j];
      j--;
    }
    arr[j + 1] = key;
  }
}
```
