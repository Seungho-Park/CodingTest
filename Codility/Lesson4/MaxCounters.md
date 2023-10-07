# MaxCounters

## 문제 설명
You are given N counters, initially set to 0, and you have two possible operations on them:

increase(X) − counter X is increased by 1,
max counter − all counters are set to the maximum value of any counter.
A non-empty array A of M integers is given. This array represents consecutive operations:

if A[K] = X, such that 1 ≤ X ≤ N, then operation K is increase(X),
if A[K] = N + 1 then operation K is max counter.
For example, given integer N = 5 and array A such that:

    A[0] = 3
    A[1] = 4
    A[2] = 4
    A[3] = 6
    A[4] = 1
    A[5] = 4
    A[6] = 4
the values of the counters after each consecutive operation will be:

    (0, 0, 1, 0, 0)
    (0, 0, 1, 1, 0)
    (0, 0, 1, 2, 0)
    (2, 2, 2, 2, 2)
    (3, 2, 2, 2, 2)
    (3, 2, 2, 3, 2)
    (3, 2, 2, 4, 2)
The goal is to calculate the value of every counter after all operations.

Write a function:

    public func solution(_ N : Int, _ A : inout [Int]) -> [Int]

that, given an integer N and a non-empty array A consisting of M integers, returns a sequence of integers representing the values of the counters.

Result array should be returned as an array of integers.

## 제한사항
 - N and M are integers within the range [1..100,000];
 - each element of array A is an integer within the range [1..N + 1].

## 입출력 예
| A | result |
| - | ------ |
|[3, 4, 4, 6, 1, 4, 4]|[3, 2, 2, 4, 2]|


## 소스 코드
```Swift
import Foundation
import Glibc

// you can write to stdout for debugging purposes, e.g.
// print("this is a debug message")

public func solution(_ N : Int, _ A : inout [Int]) -> [Int] {
    // Implement your solution here
    var answer: [Int] = .init(repeating: 0, count: N)

    var maxCount = 0
    var tempMax = 0
    for i in 0..<A.count {
        let index = A[i]

        if index > N {
            maxCount = max(maxCount, tempMax)
        } else {
            let nextValue = answer[index-1] + 1
            answer[index-1] = nextValue < maxCount + 1 ? maxCount + 1 : nextValue
            tempMax = max(tempMax, answer[index-1])
        }
    }

    for i in 0..<answer.count {
        if answer[i] < maxCount {
            answer[i] = maxCount
        }
    }

    return answer
}
```

## 코드 설명
난이도는 Medium인데, 어렵지는 않았다.

크기가 N인 Int 배열을 반환하는 문제였다.

A배열 안에는 리턴할 배열(answer)의 Index가 들어있고, Index가 N보다 크면 answer의 모든 값을 answer의 값 중 제일 큰 값으로 변경,

작으면 answer[Index] += 1 하는 문제였다.

다만, 루프를 통해 answer의 값을 max로 바꾸게 되면 시간복잡도가 너무 커져 실패하므로,
따로 최대값을 저장해놨다가 모든 계산이 끝난 후 answer을 한 바퀴 돌며 최대값보다 작은 값은 최대값으로 변경해주었다.

시간복잡도는 O(N + M) - N: A의 크기, M: answer의 크기