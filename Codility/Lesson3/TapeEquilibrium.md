# TapeEquilibrium

## 문제 설명
A non-empty array A consisting of N integers is given. Array A represents numbers on a tape.

Any integer P, such that 0 < P < N, splits this tape into two non-empty parts: A[0], A[1], ..., A[P − 1] and A[P], A[P + 1], ..., A[N − 1].

The difference between the two parts is the value of: |(A[0] + A[1] + ... + A[P − 1]) − (A[P] + A[P + 1] + ... + A[N − 1])|

In other words, it is the absolute difference between the sum of the first part and the sum of the second part.

Write a function:

    public func solution(_ A : inout [Int]) -> Int

that, given a non-empty array A of N integers, returns the minimal difference that can be achieved.

## 제한사항
 - N is an integer within the range [2..100,000];
 - each element of array A is an integer within the range [−1,000..1,000].

## 입출력 예
| A | result |
| - | ------ |
|[3, 1, 2, 4, 3]|1|


## 소스 코드
```Swift
import Foundation
import Glibc

// you can write to stdout for debugging purposes, e.g.
// print("this is a debug message")

public func solution(_ A : inout [Int]) -> Int {
    // Implement your solution here

    let totalSum = A.reduce(0, +)
    var answer = 100000
    var sum = 0
    for i in 0..<A.count-1 {
        sum += A[i]

        answer = min(abs(sum - (totalSum - sum)), answer)
    }

    return answer
}
```

## 코드 설명
우선 시간복잡도는 O(N)이다.

모든 수의 합을 구해놓고 반복문을 돌며 현재 Index까지의 합을 미리 구한 뒤, 합 - (모든 수의 합 - 합) 으로 문제를 해결했다.