# 기수 정렬

기수 정렬은 비교를 사용하지 않는 정렬 알고리즘이다. 기수 정렬은 숫자의 가장 작은 자릿수 (LSD, Least Significant Digit) 또는 가장 큰 자릿수 (MSD, Most Significant Digit)부터 기수에 따라 요소를 버킷으로 분할한다. 숫자의 유효 자릿수가 둘 이상인 경우 이 프로세스를 반복하여 숫자의 모든 자릿수를 계산한다.

```js
function getMax(arr) {
  let max = 0;

  for (const el of arr) {
    if (max < el.toString().length) {
      max = el.toString().length; // 가장 큰 자릿수 (ex. 123, 1, 10000가 있다면 max는 5가 저장됨)
    }
  }

  return max;
}

function getPosition(num, place) {
  return Math.floor(Math.abs(num) / Math.pow(10, place)) % 10;
}

function radixSort(arr) {
  const max = getMax(arr);

  for (let i = 0; i < max; i++) {
    let buckets = Array.from({ length: 10 }, () => []);
    for (let j = 0; j < arr.length; j++) {
      buckets[getPosition(arr[j], i)].push(arr[j]);
    }
    arr = [].concat(...buckets);
  }

  return arr;
}
```
