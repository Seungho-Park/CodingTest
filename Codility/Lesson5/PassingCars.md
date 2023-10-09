# PassingCars

## 문제 설명
A non-empty array A consisting of N integers is given. The consecutive elements of array A represent consecutive cars on a road.

Array A contains only 0s and/or 1s:

- 0 represents a car traveling east,
- 1 represents a car traveling west.

The goal is to count passing cars. We say that a pair of cars (P, Q), where 0 ≤ P < Q < N, is passing when P is traveling to the east and Q is traveling to the west.

For example, consider array A such that:

    A[0] = 0
    A[1] = 1
    A[2] = 0
    A[3] = 1
    A[4] = 1
We have five pairs of passing cars: (0, 1), (0, 3), (0, 4), (2, 3), (2, 4).

Write a function:

public func solution(_ A : inout [Int]) -> Int

that, given a non-empty array A of N integers, returns the number of pairs of passing cars.

The function should return −1 if the number of pairs of passing cars exceeds 1,000,000,000.

## 제한사항
 - N is an integer within the range [1..100,000];
 - each element of array A is an integer that can have one of the following values: 0, 1.

## 입출력 예
| A | result |
| - | ------ |
|[0, 1, 0, 1, 1]|    5   |


## 소스 코드
```Swift
import Foundation
import Glibc

// you can write to stdout for debugging purposes, e.g.
// print("this is a debug message")

public func solution(_ A : inout [Int]) -> Int {
    // Implement your solution here
    var answer = 0
    var sumValue = 0

    for value in A {
        if value == 0 {
            sumValue += 1
        } else {
            answer += sumValue
        }

        if answer > 1000000000 {
            return -1
        }
    }

    return answer
}
```

## 코드 설명
Pair의 갯수를 구하는 문제였다.

시간복잡도는 O(N)으로 배열의 모든 요소를 돌며, 값이 0이라면 더해야 할 값을 +1 해주었고
값이 1,000,000,000을 넘어가면 -1을 return하게 하여 해결하였다.