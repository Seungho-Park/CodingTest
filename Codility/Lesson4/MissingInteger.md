# MissingInteger

## 문제 설명
This is a demo task.

Write a function:

    public func solution(_ A : inout [Int]) -> Int

that, given an array A of N integers, returns the smallest positive integer (greater than 0) that does not occur in A.

## 제한사항
 - N is an integer within the range [1..100,000];
 - each element of array A is an integer within the range [−1,000,000..1,000,000].

## 입출력 예
| A | result |
| - | ------ |
|[1, 3, 6, 4, 1, 2]|5|
|[1, 2, 3]|4|
| [−1, −3]|1|


## 소스 코드
```Swift
import Foundation
import Glibc

// you can write to stdout for debugging purposes, e.g.
// print("this is a debug message")

public func solution(_ A : inout [Int]) -> Int {
    // Implement your solution here

    var answer = 1
    let array = Set(A).filter { $0 > 0 }.sorted()

    for value in array {
        if value == answer {
            answer += 1
        } else {
            break
        }
    }

    return answer
}
```

## 코드 설명
숫자배열 A에서 0보다 큰, 연속되지 않는 숫자(빠진 숫자)를 찾는 문제였다.

배열 요소에 숫자가 중복으로 들어갈 수 있기에 Set을 통하여 중복을 제거 후 0보다 큰 숫자만 필터링 하여 오름차순 정렬.

모든 요소를 돌며 빠진 숫자를 찾았다.

시간복잡도는 O(N * log(N))