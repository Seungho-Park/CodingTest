# MinAvgTwoSlice

## 문제 설명
A non-empty array A consisting of N integers is given. A pair of integers (P, Q), such that 0 ≤ P < Q < N, is called a slice of array A (notice that the slice contains at least two elements). The average of a slice (P, Q) is the sum of A[P] + A[P + 1] + ... + A[Q] divided by the length of the slice. To be precise, the average equals (A[P] + A[P + 1] + ... + A[Q]) / (Q − P + 1).

For example, array A such that:

    A[0] = 4
    A[1] = 2
    A[2] = 2
    A[3] = 5
    A[4] = 1
    A[5] = 5
    A[6] = 8
contains the following example slices:

slice (1, 2), whose average is (2 + 2) / 2 = 2;
slice (3, 4), whose average is (5 + 1) / 2 = 3;
slice (1, 4), whose average is (2 + 2 + 5 + 1) / 4 = 2.5.
The goal is to find the starting position of a slice whose average is minimal.

Write a function:

    public func solution(_ A : inout [Int]) -> Int

that, given a non-empty array A consisting of N integers, returns the starting position of the slice with the minimal average. If there is more than one slice with a minimal average, you should return the smallest starting position of such a slice.

## 제한사항
 - N is an integer within the range [2..100,000];
 - each element of array A is an integer within the range [−10,000..10,000].

## 입출력 예
|A|result|
|-|------|
|[4, 2, 2, 5, 1, 5, 8]|1|


## 소스 코드
```Swift
import Foundation
import Glibc

// you can write to stdout for debugging purposes, e.g.
// print("this is a debug message")

public func solution(_ A : inout [Int]) -> Int {
    // Implement your solution here
    var answer = 0
    var minAvg = Double(A[0] + A[1]) / 2.0

    for i in 2..<A.count {
        let avg2 = Double(A[i-1] + A[i]) / 2.0
        let avg3 = Double(A[i-2] + A[i-1] + A[i]) / 3.0

        if avg2 < minAvg {
            minAvg = avg2
            answer = i-1
        }

        if avg3 < minAvg {
            minAvg = avg3
            answer = i-2
        }
    }

    return Int(answer)
}
```

## 코드 설명
주어진 배열 A를 Slice(P ~ Q)로 만든 뒤 가장 작은 평균값의 StartIndex를 반환하는 문제였다.

평균값은 가장 작은 수보다 큰 값을 가지기때문에 4개의 요소를 가지는 배열부터는 계산할 필요가 없다.
 (2개의 요소를 가지는 배열의 평균, 2개의 요소를 가지는 배열의 평균 중 작은 값보다 크기 때문에)

배열 요소의 전체 반복문을 돌며 2개, 3개로 나누었을 때 가장 작은 평균값의 startIndex를 반환하도록 하였다.

시간복잡도는 O(N)