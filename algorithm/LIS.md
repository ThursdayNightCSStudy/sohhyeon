# Longest Increasing Sequence (LIS) 최장 부분 증가수열

원소 n개인 배열의 일부 원소를 골라내서 만든 부분 수열 중, 각 원소가 이전 원소보다 크다는 조건을 만족하고, 그 길이가 최대인 부분 수열을 최장 증가 부분 수열이라고 한다.

최장 증가 부분 수열의 길이는 DP와 이분 탐색 등의 방법을 이용해 풀 수 있다.

## DP를 사용한 풀이

- 주어진 배열을 이중 반복문으로 탐색한다.
- dy 배열은 주어진 배열과 같은 길이를 갖고, 0으로 초기화한다.
- dy의 i번째 값은 주어진 배열의 i번째 값이 부분 수열의 마지막 원소일때, 만들 수 있는 LIS의 경우의 수를 저장한다.
- dy[0]은 arr[0]이 마지막 원소일때, 만들 수 있는 LIS의 경우의 수이므로, 1이다. (원소가 어차피 1개이니까 만들 수 있는 부분 수열 자체가 1개!)
- dy[i]는 max 값에 arr[i]를 뒤에 붙이는 것이므로 max+1이 된다.
- max에는 LIS의 길이가 저장되며, 반복문을 순회하며 갱신된다.
- answer에는 LIS의 길이 값을 저장하며 0으로 초기화한다.
- 아래와 같은 방식은 이중 반복문을 순회하기 때문에 시간 복잡도가 O(n^2)이 된다.

```js
function solution(arr) {
  const size = arr.length;
  const dy = Array.from({ length: size }, () => 0);
  let answer = 0;

  dy[0] = 1;

  for (let i = 1; i < size; i++) {
    let max = 0;
    for (let j = i - 1; j >= 0; j--) {
      if (arr[j] < arr[i] && dy[j] > max) {
        max = dy[j];
      }
    }
    dy[i] = max + 1;
    answer = Math.max(answer, dy[i]);
  }

  return answer;
}
```
