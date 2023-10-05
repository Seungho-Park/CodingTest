# CyclicRotation

## 문제 설명
An array A consisting of N integers is given. Rotation of the array means that each element is shifted right by one index, and the last element of the array is moved to the first place. For example, the rotation of array A = [3, 8, 9, 7, 6] is [6, 3, 8, 9, 7] (elements are shifted right by one index and 6 is moved to the first place).

The goal is to rotate array A K times; that is, each element of A will be shifted to the right K times.

Write a function:

public func solution(_ A : inout [Int], _ K : Int) -> [Int]

that, given an array A consisting of N integers and an integer K, returns the array A rotated K times.

## 제한사항
 - N and K are integers within the range [0..100];
 - each element of array A is an integer within the range [−1,000..1,000].

## 입출력 예
| A             | K | return        |
|---------------|---|---------------|
|[3, 8, 9, 7, 6]| 3 |[9, 7, 6, 3, 8]|
|[0, 0, 0]      | 1 |[0, 0, 0]      |
|[1, 2, 3, 4]   | 4 |[1, 2, 3, 4]   |


## 소스코드
```Swift
import Foundation
import Glibc

// you can write to stdout for debugging purposes, e.g.
// print("this is a debug message")

public func solution(_ A : inout [Int], _ K : Int) -> [Int] {
    // Implement your solution here
    if A.isEmpty {
        return []
    }

    for _ in 0..<K {
        let temp = A.removeLast()
        A.insert(temp, at: 0)
    }

    return A
}
```
그냥 간단하게 A의 마지막부터 하나씩 빼서 첫번째에 추가해주는 방식으로 해결했다.

제한사항에 A의 Size가 0~ 이어서 비었을 경우, 빈 배열을 Return하는 부분 추가.

시간복잡도는 O(K). Suffix를 사용해서 풀어도 될 거 같은데, 시간복잡도는 똑같다.