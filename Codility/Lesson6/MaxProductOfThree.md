# MaxProductOfThree

## 문제 설명
A non-empty array A consisting of N integers is given. The product of triplet (P, Q, R) equates to A[P] * A[Q] * A[R] (0 ≤ P < Q < R < N).

For example, array A such that:

    A[0] = -3
    A[1] = 1
    A[2] = 2
    A[3] = -2
    A[4] = 5
    A[5] = 6

contains the following example triplets:

(0, 1, 2), product is −3 * 1 * 2 = −6
(1, 2, 4), product is 1 * 2 * 5 = 10
(2, 4, 5), product is 2 * 5 * 6 = 60
Your goal is to find the maximal product of any triplet.

Write a function:

public func solution(_ A : inout [Int]) -> Int

that, given a non-empty array A, returns the value of the maximal product of any triplet.

## 제한사항
 - N is an integer within the range [3..100,000];
 - each element of array A is an integer within the range [−1,000..1,000].

## 입출력 예
| A | result |
| - | ------ |
|[-3, 1, 2, -2, 5, 6]|60|


## 소스 코드
```Swift
import Foundation
import Glibc

// you can write to stdout for debugging purposes, e.g.
// print("this is a debug message")

public func solution(_ A : inout [Int]) -> Int {
    // Implement your solution here
    let sorted = A.sorted()
    var answer = sorted.suffix(3).reduce(1, *)
    answer = max(answer, sorted.prefix(2).reduce(1, *) * sorted.last!)
    return answer
}
```

## 코드 설명
시간복잡도 O(N *log(N))

A 배열 요소 3개를 곱하여 가장 큰 수를 계산하는 문제.

1. A배열을 정렬한 후, 맨 뒤 3개(큰 수 3개)를 곱한 값을 구한다.
2. 제한사항을 보면 A의 요소 범위는 -1000~1000이기 때문에, 음수 2개 * 양수가 곱한 게 위 값보다 더 클 수도 있다.
3. 두 개의 값을 비교하여 큰 수를 반환.

