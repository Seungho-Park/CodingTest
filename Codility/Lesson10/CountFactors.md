# CountFactors

## 문제 설명
A positive integer D is a factor of a positive integer N if there exists an integer M such that N = D * M.

For example, 6 is a factor of 24, because M = 4 satisfies the above condition (24 = 6 * 4).

Write a function:

    public func solution(_ N : Int) -> Int

that, given a positive integer N, returns the number of its factors.

## 제한사항
 - N is an integer within the range [1..2,147,483,647].

## 입출력 예
| N | result |
| - | ------ |
|24|8|

## 소스 코드
```Swift
import Foundation
import Glibc

// you can write to stdout for debugging purposes, e.g.
// print("this is a debug message")

public func solution(_ N : Int) -> Int {
    // Implement your solution here

    let sqrt = Int(sqrt(Double(N)))

    var answer = 0
    for i in 1...sqrt {
        if N % i == 0 {
            answer += 2
        }
    }

    return answer - (sqrt * sqrt == N ? 1 : 0)
}
```

## 코드 설명
시간복잡도 O(sqrt(N))

N의 약수의 갯수를 구하는 문제

N의 제곱근을 구해 1~제곱근까지 탐색하며 N%i == 0이면 결과값에 2를 더한다.
Sqrt^2 == N일 경우, (ex. 4) 결과값에 -1을 한다.