# MaxProfit

## 문제 설명
An array A consisting of N integers is given. It contains daily prices of a stock share for a period of N consecutive days. If a single share was bought on day P and sold on day Q, where 0 ≤ P ≤ Q < N, then the profit of such transaction is equal to A[Q] − A[P], provided that A[Q] ≥ A[P]. Otherwise, the transaction brings loss of A[P] − A[Q].

For example, consider the following array A consisting of six elements such that:

    A[0] = 23171
    A[1] = 21011
    A[2] = 21123
    A[3] = 21366
    A[4] = 21013
    A[5] = 21367
If a share was bought on day 0 and sold on day 2, a loss of 2048 would occur because A[2] − A[0] = 21123 − 23171 = −2048. If a share was bought on day 4 and sold on day 5, a profit of 354 would occur because A[5] − A[4] = 21367 − 21013 = 354. Maximum possible profit was 356. It would occur if a share was bought on day 1 and sold on day 5.

Write a function,

    public func solution(_ A : inout [Int]) -> Int

that, given an array A consisting of N integers containing daily prices of a stock share for a period of N consecutive days, returns the maximum possible profit from one transaction during this period. The function should return 0 if it was impossible to gain any profit.

## 제한사항
 - N is an integer within the range [0..400,000];
 - each element of array A is an integer within the range [0..200,000].

## 입출력 예
| A | result |
| - | ------ |
|[23171, 21011, 21123, 21366, 21013, 21367]|356|

## 소스 코드
```Swift
import Foundation
import Glibc

// you can write to stdout for debugging purposes, e.g.
// print("this is a debug message")

public func solution(_ A : inout [Int]) -> Int {
    // Implement your solution here
    if A.count <= 1 {
        return 0
    }

    var answer = 0
    var minValue = A.first!
    for value in A {
        if minValue > value {
            minValue = value
        } else {
            answer = max(value - minValue, answer)
        }
    }

    return answer
}
```

## 코드 설명
시간복잡도 O(N)

가장 큰 이득을 낼 수 있는 값을 구하는 문제.

해결법은 간단한데, 가장 큰 이득은 가장 큰 값 - 가장 작은 값을 하면 되므로 배열의 요소를 돌며, 작은 값이 나오면 작은 값을 갱신,

아니면 요소 - 작은값을 해서 구하면 된다.