# 거품 정렬

거품 정렬은 탄산수에서 거품의 움직임을 모방한 알고리즘으로 거품은 데이터 구조의 요소를 나타낸다. 큰 거품이 작은 거품보다 먼저 표면에 도달하는 것과 마찬가지로, 데이터 구조를 반복하고 각 주기마다 현재 요소를 다음 요소와 비교하여 순서가 잘못된 경우 교환한다.

가장 쉽게 구현할 수 있지만 효율적이진 않다.

시간복잡도는 이중 반복문을 실행해야하므로 O(n^2)을 갖는다.

```js
// 정렬에 사용되는 일반적인 헬퍼 함수
function swap(arr, idx1, idx2) {
  const temp = arr[idx1];
  arr[idx1] = arr[idx2];
  arr[idx2] = temp;
}

function bubbleSort(arr) {
  for (let i = 0; i < arr.length; i++) {
    for (let j = 0; j < arr.length - i - 1; j++) {
      // j는 기징 정렬되지 않은 가장 마지막 요소까지만
      if (arr[j] > arr[j + 1]) {
        // 부등호가 반대(<)이면 내림차순
        swap(arr, j, j + 1);
      }
    }
  }
  return arr;
}
```
