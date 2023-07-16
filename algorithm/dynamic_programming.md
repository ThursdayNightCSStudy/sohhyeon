# Divide and Conquer

분할 정복 프로그래밍은 크고 복잡한 문제를 작은 단위로 나눠서 해결한 후 다시 합치는 알고리즘이다. Top-Down 방식으로 재귀함수를 사용해서 구현하며 대표적인 에시로 merge sort가 있다.

# Dynamic Programming

다이나믹 프로그래밍이란 <b>하나의 문제를 한 번만</b> 풀도록 하는 알고리즘이다. Top-Down과 Bottom-Up으로 문제를 모두 풀 수 있다. Divide and Conquer와 비슷하지만, Memoization을 사용해 작은 문제의 해결된 값을 저장하고 있으므로, 작은 문제를 중복해서 해결하지 않는다는 점에서 다르다.
DP로 풀 수 있는 문제의 전제 조건은 첫째로 큰 문제를 작은 문제로 나눌 수 있는지, 둘째로 작은 문제에서 구한 답이 그것을 포함하는 큰 문제에서도 동일한지이다. (Optimal substructure: 궁극적인 솔루션이 더 작은 문제의 최적의 솔루션으로 이루어져 있다)

가장 대표적인 예시로는 Matrix Chain Multiplication(MCM) 문제와 Longest Common Subsequence (LCS) 문제가 있다. 두 문제 모두 최적의 솔루션을 배열에 저장해 놓고, 그 다음 최적의 솔루션을 결정하는 방식을 가지고 있으므로 DP를 적용할 수 있다.

## Divide and Conquer와의 차이점

> Divide and Conquer

- Divide (문제를 여러개의 하위 문제로 나누고) Conquer(각 하위 문제를 재귀적으로 해결하고) Combine(각 하위 문제의 풀이를 사용해 상위 문제를 해결한다.)을 반복한다.
- Top-Down 방식이다.
- DP에 비해 하위 문제 해결에 중복이 발생하므로 시간이 오래 걸린다.
- 각 하위 문제는 (서로 동일하더라도) 독립적이다. (independent)

> Dynamic Programming

- Top-Down과 Bottom-Up 방식이 모두 가능하다.
- 하위 문제들의 결과값을 배열에 저장해두고, 동일한 문제는 중복해서 계산하지 않는다. (Memoization)
- 각 하위 문제는 상호 의존적이다. (interindependent)

# Dynamic Programming 구현

## Top-Down (Memoization + 재귀)

다음은 Top-Down 방식으로 피보나치 수열을 계산하는 함수이다. 첫번째 예시는 매번 하위 문제를 다시 계산하므로 Dynamic Programming을 사용한 풀이라고 볼 수 없다. 두 번째 예시에서는 memo라는 배열에 결과값을 저장하고, 동일한 하위 문제를 중복해서 계산하지 않고 있다.

```js
// 메모이제이션 사용x. 시간복잡도 최악
function fibonacci(n) {
  if (n <= 1) {
    return 1;
  }
  return fibonacci(n - 1) + fibonacci(n - 2);
}

// 메모이제이션 사용.
const memo = [0, 1];
function fibonacci(n) {
  if (!memo[n]) {
    memo[n] = fibonacci(n - 1) + fibonacci(n - 1);
  }
  return memo[n];
}
```

## Bottom-Up (반복문)

다음은 Bottom-Up 방식으로 피보나치 수열을 계산하는 함수이다. Top-Down과 다르게 재귀함수를 사용하지 않고, 작은 문제들을 먼저 해결한 후에 배열에 저장한다.

```js
function fibonacci(n) {
  const fibo = new Array(n).fill(0);
  fibo[0] = 1;
  fibo[1] = 1;

  for (let i = 2; i <= n; i++) {
    fibo[i] = fibo[i - 1] + fibo[i - 2];
  }
  return fibo[n];
}
```
