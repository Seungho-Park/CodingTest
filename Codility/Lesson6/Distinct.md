# Distinct

## 문제 설명
Write a function

public func solution(_ A : inout [Int]) -> Int

that, given an array A consisting of N integers, returns the number of distinct values in array A.

For example, given array A consisting of six elements such that:

    A[0] = 2    A[1] = 1    A[2] = 1
    A[3] = 2    A[4] = 3    A[5] = 1

the function should return 3, because there are 3 distinct values appearing in array A, namely 1, 2 and 3.

## 제한사항
 - N is an integer within the range [0..100,000];
 - each element of array A is an integer within the range [−1,000,000..1,000,000].

## 입출력 예
| A | result |
| - | ------ |
|[2, 1, 1, 2, 3, 1]|3|


## 소스 코드
```Swift
import Foundation
import Glibc

// you can write to stdout for debugging purposes, e.g.
// print("this is a debug message")

public func solution(_ A : inout [Int]) -> Int {
    // Implement your solution here
    return Set(A).count
}
```

## 코드 설명
배열 A에서 중복요소를 제외한 요소의 갯수를 리턴하는 문제였다.

간단하게 Set을 통해 중복 요소를 제거 후 Count로 갯수를 반환하였다.

시간복잡도는 O(N)