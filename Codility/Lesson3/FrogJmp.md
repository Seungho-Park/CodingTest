# FrogJmp

## 문제 설명
A small frog wants to get to the other side of the road. The frog is currently located at position X and wants to get to a position greater than or equal to Y. The small frog always jumps a fixed distance, D.

Count the minimal number of jumps that the small frog must perform to reach its target.

Write a function:

    public func solution(_ X : Int, _ Y : Int, _ D : Int) -> Int

that, given three integers X, Y and D, returns the minimal number of jumps from position X to a position equal to or greater than Y.

## 제한사항
 - X, Y and D are integers within the range [1..1,000,000,000];
 - X ≤ Y.

## 입출력 예
| X | Y | D | result |
| - | - | - | ------ |
| 10| 85| 30|    3   |


## 소스 코드
```Swift
import Foundation
import Glibc

// you can write to stdout for debugging purposes, e.g.
// print("this is a debug message")

public func solution(_ X : Int, _ Y : Int, _ D : Int) -> Int {
    // Implement your solution here
    return D * ((Y-X)/D) >= Y-X ? ((Y-X)/D) : ((Y-X)/D) + 1
}
```

## 코드 설명
X 좌표에 있는 개구리가 D만큼 몇 번 점프를 뛰어야 Y보다 크거나 같아지는지 계산하는 문제이다.
단순 반복문으로 계산할 경우, X, Y, D의 데이터 크기가 [1..1,000,000,000]이기 때문에 시간초과가 나올 거 같아
계산으로 문제를 풀었다.

시간복잡도는 O(1)