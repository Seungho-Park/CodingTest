# OddOccurrencesInArray

## 문제 설명
A non-empty array A consisting of N integers is given. The array contains an odd number of elements, and each element of the array can be paired with another element that has the same value, except for one element that is left unpaired.

For example, in array A such that:

  A[0] = 9  A[1] = 3  A[2] = 9

  A[3] = 3  A[4] = 9  A[5] = 7

  A[6] = 9

the elements at indexes 0 and 2 have value 9,
the elements at indexes 1 and 3 have value 3,
the elements at indexes 4 and 6 have value 9,
the element at index 5 has value 7 and is unpaired.
Write a function:

public func solution(_ A : inout [Int]) -> Int

that, given an array A consisting of N integers fulfilling the above conditions, returns the value of the unpaired element.

## 제한사항
 - N is an odd integer within the range [1..1,000,000];
 - each element of array A is an integer within the range [1..1,000,000,000];
 - all but one of the values in A occur an even number of times.

## 입출력 예
| A                   | return        |
|---------------------|---------------|
|[9, 3, 9, 3, 9, 7, 9]|7              |


## 첫번째 풀이 - 실패
```Swift
import Foundation
import Glibc

// you can write to stdout for debugging purposes, e.g.
// print("this is a debug message")

public func solution(_ A : inout [Int]) -> Int {
    // Implement your solution here
    var stack: [Int] = []
    A.sort()

    for value in A {
        if let last = stack.last, last == value {
            stack.removeLast()
        } else {
            stack.append(value)
        }
    }

    return stack.first!
}
```
A를 정렬시킨 후 Stack에 넣어 같으면 빼고, 없으면 집어넣은 후

스택에 첫번째 값을 return하도록 짰다.
해당 코드의 경우 정렬하는 부분의 시간복잡도가 O(N*log(N))이라 시간초과로 실패.

## 두번째 풀이 - 성공
```Swift
import Foundation
import Glibc

// you can write to stdout for debugging purposes, e.g.
// print("this is a debug message")

public func solution(_ A : inout [Int]) -> Int {
    // Implement your solution here
    var set: Set<Int> = .init()

    for value in A {
        if set.contains(value) {
            set.remove(value)
        } else {
            set.insert(value)
        }
    }

    return set.first!
}
```
Set을 활용하여 값이 있는지 체크 후 값이 있으면 삭제, 없으면 추가하는 방식으로 해결했다.
Set은 Contains를 실행할 때, 시간복잡도가 상수로 O(1) 만큼만 걸리기 때문에 시간복잡도는 O(N)

## 참고 - 다른사람 코드
```Swift
import Foundation
import Glibc

// you can write to stdout for debugging purposes, e.g.
// print("this is a debug message")

public func solution(_ A : inout [Int]) -> Int {
    // Implement your solution here
    var answer = 0

    for value in A {
        answer = answer ^ value
    }

    return answer
}
```
XOR연산을 활용하여 간단하게 해결하였다.

시간복잡도는 O(N)