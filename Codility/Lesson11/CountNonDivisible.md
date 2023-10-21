# CountNonDivisible

## 문제 설명
You are given an array A consisting of N integers.

For each number A[i] such that 0 ≤ i < N, we want to count the number of elements of the array that are not the divisors of A[i]. We say that these elements are non-divisors.

For example, consider integer N = 5 and array A such that:

    A[0] = 3
    A[1] = 1
    A[2] = 2
    A[3] = 3
    A[4] = 6
For the following elements:

- A[0] = 3, the non-divisors are: 2, 6,
- A[1] = 1, the non-divisors are: 3, 2, 3, 6,
- A[2] = 2, the non-divisors are: 3, 3, 6,
- A[3] = 3, the non-divisors are: 2, 6,
- A[4] = 6, there aren't any non-divisors.

Write a function:

    public func solution(_ A : inout [Int]) -> [Int]

that, given an array A consisting of N integers, returns a sequence of integers representing the amount of non-divisors.

Result array should be returned as an array of integers.

## 제한사항
 - N is an integer within the range [1..50,000];
 - each element of array A is an integer within the range [1..2 * N].

## 입출력 예
| A | result |
| - | ------ |
|[3, 1, 2, 3, 6]]|[2, 4, 3, 2, 0]|

## 소스 코드
```Swift
import Foundation
import Glibc

// you can write to stdout for debugging purposes, e.g.
// print("this is a debug message")

public func solution(_ A : inout [Int]) -> [Int] {
    // Implement your solution here
    let elementsCount = A.count
    var elements: [Int] = .init(repeating: 0, count: elementsCount * 2+1)
    var answer: [Int] = .init(repeating:0, count: elementsCount)
    var dict: [Int:Int] = [:]


    for value in A {
        elements[value] += 1
    }

    for i in 0..<A.count {
        let value = A[i]

        if dict[value] == nil {
            let sqrt = Int(sqrt(Double(value)))
            var divisorCount = 0
            for j in 1...sqrt {
                if value % j == 0 {
                    divisorCount += elements[j]

                    if value / j != j {
                        divisorCount += elements[value/j]
                    }
                }
            }

            dict[value] = elementsCount - divisorCount
        }

        answer[i] = dict[value] ?? 0
    }

    return answer
}
```

## 코드 설명
시간복잡도 O(N * log(N))

첫번째 시도에서는 나눠지지 않는 수의 갯수를 저장할 Dictionary하나를 선언한 뒤,
루프 안에 루프로 배열의 모든 요소를 돌며 탐색을 시도했다.
```Swift
for i in 0..<A.count {
    let value = A[i]
    for j in 0..<A.count {
        if j == i {
            continue
        }
    }

    if value % A[j] != 0 {
        count += 1
    }
}
```

당연히 퍼포먼스 점수 미달로 75% 정답률로 실패.

문제를 다시 파악해보았다.

제한조건에서 A의 각 요소 크기는 1 ~ N*2다.
나눠지지 않는 수는 약수가 아닌 수를 말하는 거니까, A의 범위 안에 있는 약수를 먼저 구한 후 그 수를 빼주기로 했다.

우선 각 요소의 등장횟수를 기록할 배열을 하나 선언, 크기는 제한조건처럼 N*2 + 1로 잡았다.

각 요소의 등장횟수를 기록한 후, A 배열을 순회하며 1~각 요소의 제곱근만큼 돌며
 - 제곱근만큼 도는 이유는 예를들어 요소가 16일때 약수는 [1, 2, 4, 8 ,16]이다. 1, 2, 4까지만 구하면 8, 16도 약수라는걸 알 수 있으니까.

해당수가 약수라면 elements[약수]의 갯수를 기록
또 A[i] / j != j면 (ex, 16일때는 4, 4로 같은 경우도 있지만, 2, 8처럼 다른 경우)

elements[A[i]/j]의 등장횟수도 더한다.

마지막으로 A.count - 약수의 갯수를 빼면 해당 수의 약수가 아닌 수의 갯수를 구할 수 있다.

시간복잡도는 O(N * log(N))이었으나, 해당 코드 역시 마지막 퍼포먼스 테스트를 실패하여 88%의 정답률만 보였다.

이유를 보니 A의 크기가 50,000이고, 모든 요소가 같은 요소일 때 시간초과가 발생.

Dictionary를 추가하여 한 번 구했던 요소는 다시 계산하지 않도록하여 해결했다.