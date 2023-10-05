# PermMissingElem

## 문제 설명
An array A consisting of N different integers is given. The array contains integers in the range [1..(N + 1)], which means that exactly one element is missing.

Your goal is to find that missing element.

Write a function:

    public func solution(_ A : inout [Int]) -> Int

that, given an array A, returns the value of the missing element.

## 제한사항
 - N is an integer within the range [0..100,000];
 - the elements of A are all distinct;
 - each element of array A is an integer within the range [1..(N + 1)].

## 입출력 예
|      A     | result |
| ---------- | ------ |
|[2, 3, 1, 5]|    4   |


## 소스 코드
```Swift
import Foundation
import Glibc

// you can write to stdout for debugging purposes, e.g.
// print("this is a debug message")

public func solution(_ A : inout [Int]) -> Int {
    // Implement your solution here
    var answer = 1
    for value in A.sorted() {
        if answer == value {
            answer += 1
        } else {
            break
        }
    }

    return answer
}
```

## 코드 설명
A를 정렬시킨 후, 값이 1부터 시작해서 있다면 +1 없다면 그 값을 return하도록 구현하였다.

의도한 부분은 아니지만, 이렇게 풀었더니 빈 배열이 들어왔을 경우도 해결되었다. (제한사항을 잘 읽어보자.)

시간복잡도는 O(n * log(N)), 최대 O(N)이다.