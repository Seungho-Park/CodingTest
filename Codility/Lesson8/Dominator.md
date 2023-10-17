# Dominator

## 문제 설명
An array A consisting of N integers is given. The dominator of array A is the value that occurs in more than half of the elements of A.

For example, consider array A such that

    A[0] = 3    A[1] = 4    A[2] =  3
    A[3] = 2    A[4] = 3    A[5] = -1
    A[6] = 3    A[7] = 3

The dominator of A is 3 because it occurs in 5 out of 8 elements of A (namely in those with indices 0, 2, 4, 6 and 7) and 5 is more than a half of 8.

Write a function

    public func solution(_ A : inout [Int]) -> Int

that, given an array A consisting of N integers, returns index of any element of array A in which the dominator of A occurs. The function should return −1 if array A does not have a dominator.

## 제한사항
 - N is an integer within the range [0..100,000];
 - each element of array A is an integer within the range [−2,147,483,648..2,147,483,647].

## 입출력 예
| A | result |
| - | ------ |
|[3, 4, 3, 2, 3, -1, 3, 3]|0 or 2 or 4 or 6 or 7|

## 소스 코드
```Swift
import Foundation
import Glibc

// you can write to stdout for debugging purposes, e.g.
// print("this is a debug message")

public func solution(_ A : inout [Int]) -> Int {
    // Implement your solution here
    var dict: [Int:Int] = [:]

    for i in 0..<A.count {
        var value = dict[A[i]] ?? 0
        value += 1

        if value > A.count/2 {
            return i
        } else {
            dict[A[i]] = value
        }
    }

    return -1
}
```

## 코드 설명
시간복잡도 O(N)

요소의 갯수가 배열 크기의 절반을 넘는 요소의 index중 아무거나 반환하면 되는 문제.

요소의 등장 횟수를 저장할 Dictionary를 하나 만들었다.
 * 주의점: Dictionary의 Value가 요소의 index를 저장하기 위해 배열로 만들 경우, index를 추가하는 부분에서 배열 복사 때문에 시간복잡도가 증가함.

A 배열을 돌며 각 요소의 등장 횟수를 확인하고 배열 크기의 절반을 넘어가면 index를 return.

배열 끝까지 돌았는데도 없으면 -1 return.