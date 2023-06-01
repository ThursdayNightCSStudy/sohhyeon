# 계수 정렬

계수 정렬은 숫자에 대해서만 동작하고 특정 범위가 주어져야 한다. 항목들을 교환(swap)하면서 정렬하는 대신 배열의 등장 횟수를 센다. 각 항목의 등장 횟수를 센 다음 해당 등장 횟수를 사용해 새로운 배열을 생성할 수 있다.

제한된 범위의 정수를 정렬할 때는 계수 정렬이 효율적이며 시간 복잡도는 O(n)이다.

```js
function countSort(arr) {
  const hash = {};
  const countArr = [];

  for (let i = 0; i < arr.length; i++) {
    if (!hash[arr[i]]) {
      hash[arr[i]] = 1;
    } else {
      hash[arr[i]]++;
    }
  }

  for (const key in hash) {
    for (let i = 0; i < hash[key]; i++) {
      countArr.push(parseInt(key));
    }
  }

  return countArr;
}
```
