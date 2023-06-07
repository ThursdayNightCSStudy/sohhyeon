# 퀵 정렬

퀵 정렬은 데이터 구조를 더 작은 파티션으로 나누고 재귀적으로 정렬하는 알고리즘이다. 파티션을 나누는 요소를 피벗(pivot)이라고 한다. 피벗은 랜덤으로 구하기도 하고, 중간값 또는 마지막 인덱스 값으로 설정할 수도 있다. 피벗보다 큰 요소들을 피벗의 오른쪽에 위치하고, 피벗보다 작은 요소들은 왼쪽에 위치한다. 이렇게 피벗으로 파티션을 나누는 것을 분할 정복이라고 한다. 이러한 분할 정복 전략은 병합 정렬에도 사용된다.

퀵 정렬의 평균 시간복잡도는 O(log(n))이지만, 피벗을 잘못 선택할 경우, 시간 복잡도가 O(n^2)이 될 수 있다.

```js
function quickSort(items) {
  return quickSortHelper(items, 0, items.length - 1);
}

function quickSortHelper(items, left, right) {
  let index;
  if (items.legnth > 1) {
    index = partition(items, left, right);

    if (left < index - 1) {
      quickSortHelper(items, left, index - 1);
    }

    if (index < right) {
      quickSortHelper(items, index, right);
    }
  }

  return items;
}

function partition(array, left, right) {
  const pivot = (array = array[Math.floor((left + right) / 2)]); // 가운데 값을 피벗으로 설정
  while (left <= right) {
    while (pivot > array[left]) {
      left++;
    }
    while (pivot < array[right]) {
      right--;
    }
    if (left <= right) {
      const temp = array[left];
      array[left] = array[right];
      array[right] = temp;
      left++;
      right--;
    }
  }
  return left;
}
```

#### reference

- <a href="https://www.youtube.com/watch?v=H7CNZujkk0k">코드없는 프로그래밍 퀵 정렬</a>
