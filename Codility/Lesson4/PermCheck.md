# PermCheck

## 문제 설명
A non-empty array A consisting of N integers is given.

A permutation is a sequence containing each element from 1 to N once, and only once.

For example, array A such that:

    A[0] = 4
    A[1] = 1
    A[2] = 3
    A[3] = 2
is a permutation, but array A such that:

    A[0] = 4
    A[1] = 1
    A[2] = 3
is not a permutation, because value 2 is missing.

The goal is to check whether array A is a permutation.

Write a function:

public func solution(_ A : inout [Int]) -> Int

that, given an array A, returns 1 if array A is a permutation and 0 if it is not.

## 제한사항
 - N is an integer within the range [1..100,000];
 - each element of array A is an integer within the range [1..1,000,000,000].

## 입출력 예
| A | result |
| - | ------ |
|[4, 1, 3, 2]|    1   |
|[4, 1, 3]|    0   |


## 소스 코드
```Swift
import Foundation
import Glibc

// you can write to stdout for debugging purposes, e.g.
// print("this is a debug message")

public func solution(_ A : inout [Int]) -> Int {
    // Implement your solution here
    A.sort()

    var number = 1

    for value in A {
        if value == number {
            number += 1
        } else {
            return 0
        }
    }

    return 1
}
```

## 코드 설명
Int 배열 A가 순열인지 확인하여, 순열이면 1을 아니면 0을 반환하는 문제이다.

간단하게 A를 오름차순으로 정렬하여 처음부터 끝까지 돌며 순열이 맞는지 확인하여 맞으면 1을, 아니면 0을 리턴하도록 하였다.

시간복잡도는 O(N * log(N))