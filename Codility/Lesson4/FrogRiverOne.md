# FrogRiverOne

## 문제 설명
A small frog wants to get to the other side of a river. The frog is initially located on one bank of the river (position 0) and wants to get to the opposite bank (position X+1). Leaves fall from a tree onto the surface of the river.

You are given an array A consisting of N integers representing the falling leaves. A[K] represents the position where one leaf falls at time K, measured in seconds.

The goal is to find the earliest time when the frog can jump to the other side of the river. The frog can cross only when leaves appear at every position across the river from 1 to X (that is, we want to find the earliest moment when all the positions from 1 to X are covered by leaves). You may assume that the speed of the current in the river is negligibly small, i.e. the leaves do not change their positions once they fall in the river.

For example, you are given integer X = 5 and array A such that:

    A[0] = 1
    A[1] = 3
    A[2] = 1
    A[3] = 4
    A[4] = 2
    A[5] = 3
    A[6] = 5
    A[7] = 4
In second 6, a leaf falls into position 5. This is the earliest time when leaves appear in every position across the river.

Write a function:

    public func solution(_ X : Int, _ A : inout [Int]) -> Int

that, given a non-empty array A consisting of N integers and integer X, returns the earliest time when the frog can jump to the other side of the river.

If the frog is never able to jump to the other side of the river, the function should return −1.

## 제한사항
 - N and X are integers within the range [1..100,000];
 - each element of array A is an integer within the range [1..X].

## 입출력 예
| A | X | result |
| - | - | ------ |
|[1, 3, 1, 4, 2, 5, 3, 5, 4]| 5|    6   |


## 소스 코드
```Swift
import Foundation
import Glibc

// you can write to stdout for debugging purposes, e.g.
// print("this is a debug message")

public func solution(_ X : Int, _ A : inout [Int]) -> Int {
    // Implement your solution here
    var set: Set<Int> = .init()

    var answer = -1
    for i in 0..<A.count {
        if A[i] <= X {
            if !set.contains(A[i]) {
                set.insert(A[i])
            }
        }

        if set.count == X {
            answer = i
            break
        }
    }

    return answer
}
```

## 코드 설명
0의 위치에 있는 개구리가 X로 이동할 수 있는 최소 시간을 구하는 문제이다.

1~X까지 모든 수가 나왔을 때를 구하면 되는 문제로 Set을 이용하여 시간복잡도 O(N)으로 문제를 해결하였다.