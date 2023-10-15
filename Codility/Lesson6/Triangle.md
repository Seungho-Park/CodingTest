# Triangle

## 문제 설명
An array A consisting of N integers is given. A triplet (P, Q, R) is triangular if 0 ≤ P < Q < R < N and:

    A[P] + A[Q] > A[R],
    A[Q] + A[R] > A[P],
    A[R] + A[P] > A[Q].
For example, consider array A such that:

    A[0] = 10    A[1] = 2    A[2] = 5
    A[3] = 1     A[4] = 8    A[5] = 20

Triplet (0, 2, 4) is triangular.

Write a function:

    public func solution(_ A : inout [Int]) -> Int

that, given an array A consisting of N integers, returns 1 if there exists a triangular triplet for this array and returns 0 otherwise.

## 제한사항
 - N is an integer within the range [0..100,000];
 - each element of array A is an integer within the range [−2,147,483,648..2,147,483,647].

## 입출력 예
| A | result |
| - | ------ |
|[10, 2, 5, 1, 8, 20]|1|


## 소스 코드
```Swift
import Foundation
import Glibc

// you can write to stdout for debugging purposes, e.g.
// print("this is a debug message")

public func solution(_ A : inout [Int]) -> Int {
    // Implement your solution here

    if A.count < 3 {
        return 0
    }

    A.sort()
    for i in 0..<A.count-2 {
        if A[i+1] > A[i+2] - A[i] {
            return 1
        }
    }

    return 0
}
```

## 코드 설명
시간복잡도 O(N *log(N))

A 배열 요소 3개를 뽑아내어, 2개를 더한 값이 나머지 하나의 값보다 큰 것이 있는지 찾는 문제다.

다만 제한사항에 배열의 크기는 0~이므로 배열의 크기가 3보다 작으면 3개를 뽑아낼 수 없으므로 0을 반환하고,
A를 정렬한 후 첫번째 index부터 3개를 뽑아내어 비교를 한다.

제한사항의 값 범위가 커 오버플로우가 발생할 수 있으므로 식을 변형하여 문제를 해결하였다.
