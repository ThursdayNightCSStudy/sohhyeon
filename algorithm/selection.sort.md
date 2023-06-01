# 선택 정렬

선택 정렬은 가장 작은 항목을 찾아서 해당 항목을 배열의 현 위치에 삽입하는 방식으로 동작한다.

다음 함수에서 배열을 순회하는 for loop가 있고, 최소 항목을 얻기 위해 검색하는 중첩 for loop가 있다.

시간 복잡도는 이중 반복문을 실행해야하므로 O(n^2)을 갖는다.

```js
function selectgionSort(arr) {
  for (let i = 0; i < arr.length; i++) {
    let min = i; // 최소 항목을 현재 위치(인덱스)로 설정
    for (let j = i + 1; j < arr.length; j++) {
      if (arr[min] > arr[j]) {
        // 현재 위치를 제외한 그 이후의 배열을 탐색하면서 최소 항목의 위치를 찾는다.
        min = j;
      }
    }
    if (i !== min) {
      swap(arr, i, min); // 현재 위치가 최소 항목 위치가 아니라면 항목을 교환한다.
    }
  }

  return arr;
}
```
