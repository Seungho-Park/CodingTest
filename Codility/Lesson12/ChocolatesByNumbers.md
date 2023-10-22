# ChocolatesByNumbers

## 문제 설명
Two positive integers N and M are given. Integer N represents the number of chocolates arranged in a circle, numbered from 0 to N − 1.

You start to eat the chocolates. After eating a chocolate you leave only a wrapper.

You begin with eating chocolate number 0. Then you omit the next M − 1 chocolates or wrappers on the circle, and eat the following one.

More precisely, if you ate chocolate number X, then you will next eat the chocolate with number (X + M) modulo N (remainder of division).

You stop eating when you encounter an empty wrapper.

For example, given integers N = 10 and M = 4. You will eat the following chocolates: 0, 4, 8, 2, 6.

The goal is to count the number of chocolates that you will eat, following the above rules.

Write a function:

    public func solution(_ N : Int, _ M : Int) -> Int

that, given two positive integers N and M, returns the number of chocolates that you will eat.

## 제한사항
 - N and M are integers within the range [1..1,000,000,000].

## 입출력 예
|N|M|result|
|-|-|-|
|10|4|5|

## 소스 코드
```Swift
import Foundation
import Glibc

// you can write to stdout for debugging purposes, e.g.
// print("this is a debug message")

public func solution(_ N : Int, _ M : Int) -> Int {
    // Implement your solution here
    return N / gcd(N, M)
}

func gcd(_ n: Int, _ m: Int)-> Int {
    if m == 0 { return n }
    return gcd(m, n % m)
}
```

## 코드 설명
유클리드 호제법을 통하여 두 수의 최대공약수를 구한 뒤 N / 최대공약수가 결과값이다.
초콜릿을 먹는 순서를 보면 0(10), 4, 8, 2, 6 인데 보면 모두 10의 약수이다.

그래서 N과 M의 최대공약수를 구한 후 N / 최대공약수가 정답.