# MaxSliceSum

## 문제 설명
A non-empty array A consisting of N integers is given. A pair of integers (P, Q), such that 0 ≤ P ≤ Q < N, is called a slice of array A. The sum of a slice (P, Q) is the total of A[P] + A[P+1] + ... + A[Q].

Write a function:

    public func solution(_ A : inout [Int]) -> Int

that, given an array A consisting of N integers, returns the maximum sum of any slice of A.

## 제한사항
 - N is an integer within the range [1..1,000,000];
 - each element of array A is an integer within the range [−1,000,000..1,000,000];
 - the result will be an integer within the range [−2,147,483,648..2,147,483,647].

## 입출력 예
| A | result |
| - | ------ |
|[3, 2, -6, 4, 0]|5|

## 소스 코드
```Swift
import Foundation
import Glibc

// you can write to stdout for debugging purposes, e.g.
// print("this is a debug message")

public func solution(_ A : inout [Int]) -> Int {
    // Implement your solution here
    var answer = Int.min

    var sum = 0
    for value in A {
        sum += value

        answer = max(sum, answer)
        sum = max(0, sum)
    }

    return answer
}
```

## 코드 설명
시간복잡도 O(N)

간단하면서도 복잡한 문제.

제한사항의 정답 범위가 상당히 넓으므로, answer의 값을 Int.min으로 설정한 후 시작하였다.

배열을 순회하며 Sum에 더한 후, answer과 비교, 더 큰 값으로 answer을 갱신한다.

이후 sum이 음수일 경우 다음에 뭐가 나와도 (양수가 나오면 양수 하나만 하는 것보다 작고, 음수가 나오면 더 작아짐) 작으니 음수일 경우 0을 넣는다.

끝까지 돌면 정답 나옴,