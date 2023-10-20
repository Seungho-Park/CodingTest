# MinPerimeterRectangle

## 문제 설명
An integer N is given, representing the area of some rectangle.

The area of a rectangle whose sides are of length A and B is A * B, and the perimeter is 2 * (A + B).

The goal is to find the minimal perimeter of any rectangle whose area equals N. The sides of this rectangle should be only integers.

For example, given integer N = 30, rectangles of area 30 are:

    (1, 30), with a perimeter of 62,
    (2, 15), with a perimeter of 34,
    (3, 10), with a perimeter of 26,
    (5, 6), with a perimeter of 22.
Write a function:

    public func solution(_ N : Int) -> Int

that, given an integer N, returns the minimal perimeter of any rectangle whose area is exactly equal to N.

## 제한사항
 - N is an integer within the range [1..1,000,000,000].

## 입출력 예
| N | result |
| - | ------ |
|30|22|

## 소스 코드
```Swift
import Foundation
import Glibc

// you can write to stdout for debugging purposes, e.g.
// print("this is a debug message")

public func solution(_ N : Int) -> Int {
    // Implement your solution here
    let sqrt = Int(sqrt(Double(N)))

    var value = 0
    for i in stride(from: sqrt, through: 1, by: -1) {
        if N % i == 0 {
            value = i
            break
        }
    }

    return 2 * (value + N/value)
}
```

## 코드 설명
시간복잡도 O(sqrt(N))

CountFactors 문제의 응용판 버전이다.

직사각형의 넓이 N이 주어지면 직사격형의 최소 둘레를 구하는 문제로 둘레는 2 * (A + B)로 구할 수 있다.

N의 제곱근부터 1까지 돌며 N % i 가 0이 되는 순간 i 값을 A로 두고, 2 * (A + N / A)하면 정답.