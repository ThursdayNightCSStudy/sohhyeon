# 퀵 정렬

퀵 정렬도 마찬가지로 분할정복을 사용한다. 병합 정렬은 주어진 배열을 반으로 나눠 분할했다면, 퀵 정렬은 배열을 파티셔닝으로 분할한다. 파티셔닝은, 
정렬할 임의의 수를 고르고, 그 수를 기준으로 나머지 수를 비교해서, 작은 수는 왼쪽, 큰 수는 오른쪽으로 보내는 것을 말한다. 당연하게도 파티셔닝을 한 번 한다고 해서, 배열이 완벽하게 정렬되지는 않는다. 다만, 기준이 된 숫자는 정렬이 된 상태가 된다. 이렇게 기준이 된 숫자를 피벗(pivot)이라고 한다.

퀵 정렬에서 파티셔닝으로 분할한다고 설명했는데, 파티셔닝의 시간 복잡도는 무엇일까? 피벗을 기준으로 숫자를 왼쪽으로, 오른쪽으로 보내야하므로, 피벗과 그 외의 숫자를 1번씩 모두 비교해야한다. 따라서 파티셔닝의 시간 복잡도는 O(n)이다. 그리고, 파티셔닝은 재귀함수로 호출될때마다 실행된다.

그렇다면, 재귀함수는 몇 번 호출될까?

퀵 정렬과 마찬가지로 분할 정복 방식을 사용하는 병합 정렬의 경우, 배열이 반드시 반으로 분할되기 때문에 단계가 logN으로 고정된다. 하지만, 파티셔닝 방식을 사용한다면, 피벗이 무엇이 되느냐에 따라 단계가 달라지고, 단계가 달라진다는 것은 재귀함수가 호출되는 횟수가 달라진다는 것이다. 

- 최선의 경우: 피벗이 항상 배열의 중간값!

  배열은 항상 반으로 분할되므로, 단계는 logN이 된다.

- 최악의 경우: 피벗이 항상 배열의 최소값 또는 최대값!

  배열이 항상 1개의 원소와 나머지 원소들로 분할되고 배열은 항상 빈배열과 N-1개의 원소를 가진 배열로 분리된다. 즉, 단계는 N이 된다.
  
  ```js
  [1,3,9,8,2,7]
  pivot: 1
  왼쪽: [] // 없음
  오른쪽: [3,9,8,2,7]

  pivot: 2
  왼쪽: []
  오른쪽: [3,9,8,7]

  pivot: 3
  왼쪽: []
  오른쪽: [9,8,7]

  pivot: 7
  왼쪽: []
  오른쪽: [9,8]

  pivot: 8
  왼쪽: []
  오른쪽: [9]

  pivot: 9
  왼쪽: []
  오른쪽: []
  ```

- 평균적인 경우: 

하지만 우리가 n-1번을 쪼개는 동안 모두 최소값이나 최대값을 고를 확률은 매우작다.

n개의 배열에서 1번 최대값이나 최소값을 고를 확률은 2/n이다. 모든 파티셔닝에서 최소/최대값을 고를 확률은, (2/n)^n 이다. n이 무한히 커질 때 이 확률은 0에 수렴한다.

따라서, 매번 최대값 또는 최소값을 고르는 경우는 거의 없으므로, 평균적인 경우에는 단계가 logN이 된다.

퀵 정렬의 평균 시간복잡도는 O(log(n))이지만, 최악의 경우, 시간 복잡도는 O(n^2)이 될 수 있다.

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

# 퀵 정렬과 병합 정렬의 차이점

- 병합 정렬은 배열을 반으로 나누고, 퀵 정렬은 배열을 파티셔닝으로 나눈다.
- 퀵 정렬은 병합정렬과 달리 다른 메모리 공간을 사용하지 않는다. (오직 재귀 콜 스택을 위한 메모리만 사용됨, 그에 반면 병합정렬은 매 번 새로운 배열을 만들어 내므로 메모리 사용량이 더 큼) 병합 정렬의 공간복잡도는 O(n).
- 퀵 정렬은 파티션의 방법에 따라 최악의 경우에 O(n²) 까지 성능이 낮아질 수 있고, 평균적으로는 O(nlogn)의 성능을 보인다. 병합 정렬은 항상 O(nlogn)의 성능을 보인다.


#### reference

- <a href="https://www.youtube.com/watch?v=H7CNZujkk0k">코드없는 프로그래밍 퀵 정렬</a>
- <a href="https://velog.io/@eddy_song/quick-sort">우연성이 만드는 안정성, 퀵 정렬(Quick Sort)</a>