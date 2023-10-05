# BinaryGap

## 문제 설명
A binary gap within a positive integer N is any maximal sequence of consecutive zeros that is surrounded by ones at both ends in the binary representation of N.

For example, number 9 has binary representation 1001 and contains a binary gap of length 2. The number 529 has binary representation 1000010001 and contains two binary gaps: one of length 4 and one of length 3. The number 20 has binary representation 10100 and contains one binary gap of length 1. The number 15 has binary representation 1111 and has no binary gaps. The number 32 has binary representation 100000 and has no binary gaps.

Write a function:

public func solution(_ N : Int) -> Int

that, given a positive integer N, returns the length of its longest binary gap. The function should return 0 if N doesn't contain a binary gap.

For example, given N = 1041 the function should return 5, because N has binary representation 10000010001 and so its longest binary gap is of length 5. Given N = 32 the function should return 0, because N has binary representation '100000' and thus no binary gaps.

## 제한사항
 - N is an integer within the range [1..2,147,483,647].

## 입출력 예
|N|return|
|-|------|
|1041|5|
|32|0|


## 소스코드
```Swift
import Foundation
import Glibc

// you can write to stdout for debugging purposes, e.g.
// print("this is a debug message")

public func solution(_ N : Int) -> Int {
    // Implement your solution here
    var count = 0
    var answer = 0
    String(N, radix: 2).forEach {
        if $0 == "1" {
            answer = max(answer, count)
            count = 0
        } else {
            count += 1
        }
    }

    return answer
}
```
입력값(N)을 2진수 값으로 바꿔 1과 1 사이의 0의 갯수 중 가장 큰 갯수를 구하는 문제.

32의 경우 2진수 변환 시 100000이라 1과 1 사이에 있는 0이 없어 0을 리턴하면 되는 문제였다.

간단하게 0이 나왔을 때 count를 증가시키고, 1이 나왔을 때 max값인지 확인하여 해결하였다.
