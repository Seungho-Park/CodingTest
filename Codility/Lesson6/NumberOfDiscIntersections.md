# NumberOfDiscIntersections

## 문제 설명
We draw N discs on a plane. The discs are numbered from 0 to N − 1. An array A of N non-negative integers, specifying the radiuses of the discs, is given. The J-th disc is drawn with its center at (J, 0) and radius A[J].

We say that the J-th disc and K-th disc intersect if J ≠ K and the J-th and K-th discs have at least one common point (assuming that the discs contain their borders).

The figure below shows discs drawn for N = 6 and A as follows:

    A[0] = 1
    A[1] = 5
    A[2] = 2
    A[3] = 1
    A[4] = 4
    A[5] = 0

There are eleven (unordered) pairs of discs that intersect, namely:

- discs 1 and 4 intersect, and both intersect with all the other discs;
- disc 2 also intersects with discs 0 and 3.

Write a function:

    public func solution(_ A : inout [Int]) -> Int

that, given an array A describing N discs as explained above, returns the number of (unordered) pairs of intersecting discs. The function should return −1 if the number of intersecting pairs exceeds 10,000,000.

Given array A shown above, the function should return 11, as explained above.

## 제한사항
 - N is an integer within the range [0..100,000];
 - each element of array A is an integer within the range [0..2,147,483,647].

## 입출력 예
| A | result |
| - | ------ |
|[1, 5, 2, 1, 4, 0]|11|


## 소스 코드
```Swift
import Foundation
import Glibc

// you can write to stdout for debugging purposes, e.g.
// print("this is a debug message")

public func solution(_ A : inout [Int]) -> Int {
    // Implement your solution here
    var minArray: [Int] = []
    var maxArray: [Int] = []

    for i in 0..<A.count {
        minArray.append(i - A[i])
        maxArray.append(i + A[i])
    }
    minArray.sort()
    maxArray.sort()

    var answer = 0
    var diskCount = 0
    var maxIdx = 0
    for i in 0..<minArray.count {
        while minArray[i] > maxArray[maxIdx] {
            diskCount -= 1
            maxIdx += 1
        }

        answer += diskCount

        if answer > 10000000 {
            return -1
        }
        diskCount += 1
    }

    return answer
}
```

## 코드 설명
N개로 구성된 배열 A가 입력으로 들어온다.

중심의 값은 0~N-1이고, 이건 A의 index.
 - (ex: i = 1, A[i] = 5일 경우 중심은 1, 범위는 1-5 ~ 1+5까지)

A가 주어졌을 때, 겹치는 디스크 쌍의 갯수를 구하는 문제.

우선 i - A[i]값(minArray)과 i+A[i](maxArray)의 값들을 구한 뒤 오름차순으로 정렬시킨다.

이후 minArray를 기준으로 반복문을 돌며 minArray[i] > maxArray[maxIndex]일 경우 maxIndex를 증가시키고 Count를 증가시킨다.

아닐 경우 i의 값을 증가시키며 minArray가 maxArray보다 클 경우의 갯수를 모두 더하면 정답이 나온다.

시간복잡도는 O(N * log(N))