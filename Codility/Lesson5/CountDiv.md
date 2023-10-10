# CountDiv

## 문제 설명
Write a function:

    public func solution(_ A : Int, _ B : Int, _ K : Int) -> Int

that, given three integers A, B and K, returns the number of integers within the range [A..B] that are divisible by K, i.e.:

    { i : A ≤ i ≤ B, i mod K = 0 }

For example, for A = 6, B = 11 and K = 2, your function should return 3, because there are three numbers divisible by 2 within the range [6..11], namely 6, 8 and 10..

## 제한사항
 - A and B are integers within the range [0..2,000,000,000];
 - K is an integer within the range [1..2,000,000,000];
 - A ≤ B.

## 입출력 예
| A | B | K |result|
| - | - | - |-|
| 6 | 11| 2 |3|


## 소스 코드
```Swift
import Foundation
import Glibc

// you can write to stdout for debugging purposes, e.g.
// print("this is a debug message")

public func solution(_ A : Int, _ B : Int, _ K : Int) -> Int {
    // Implement your solution here

    return B / K - A / K + (A%K == 0 ? 1 : 0)
}
```

## 코드 설명
Integer 배열 [A...B] 요소 중 K로 나눴을 때 0이 되는 요소의 갯수를 구하는 문제였다.

제한사항을 보면 알겠지만 범위가 0~2,000,000,000이기 때문에 반복문으로 해결할 시 시간초과로 실패할 것이 분명하였기에 다른 방법으로 접근하였다.

먼저 B를 K로 나눴을 때의 갯수를 구하고 ([0~B] % K == 0) 그 숫자에다 A/K를 빼준다 ([0~A] % K == 0)

A % K가 0이 나올 경우도 있기 때문에 A%K == 0이면 구한 숫자에 +1하여 정답을 구했다.