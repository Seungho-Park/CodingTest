# CountSemiprimes

## 문제 설명
A prime is a positive integer X that has exactly two distinct divisors: 1 and X. The first few prime integers are 2, 3, 5, 7, 11 and 13.

A semiprime is a natural number that is the product of two (not necessarily distinct) prime numbers. The first few semiprimes are 4, 6, 9, 10, 14, 15, 21, 22, 25, 26.

You are given two non-empty arrays P and Q, each consisting of M integers. These arrays represent queries about the number of semiprimes within specified ranges.

Query K requires you to find the number of semiprimes within the range (P[K], Q[K]), where 1 ≤ P[K] ≤ Q[K] ≤ N.

For example, consider an integer N = 26 and arrays P, Q such that:

    P[0] = 1    Q[0] = 26
    P[1] = 4    Q[1] = 10
    P[2] = 16   Q[2] = 20
The number of semiprimes within each of these ranges is as follows:

- (1, 26) is 10,
- (4, 10) is 4,
- (16, 20) is 0.
  
Write a function:

    public func solution(_ N : Int, _ P : inout [Int], _ Q : inout [Int]) -> [Int]

that, given an integer N and two non-empty arrays P and Q consisting of M integers, returns an array consisting of M elements specifying the consecutive answers to all the queries.

## 제한사항
 - N is an integer within the range [1..50,000];
 - M is an integer within the range [1..30,000];
 - each element of arrays P and Q is an integer within the range [1..N];
 - P[i] ≤ Q[i].

## 입출력 예
| N |P|Q| result |
| - |-|-| ------ |
|26|[1, 4, 16]|[26, 10, 20]|[10, 4, 0]|

## 소스 코드
```Swift
import Foundation
import Glibc

// you can write to stdout for debugging purposes, e.g.
// print("this is a debug message")

public func solution(_ N : Int, _ P : inout [Int], _ Q : inout [Int]) -> [Int] {
    // Implement your solution here
    var isPrime: [Bool] = .init(repeating: true, count: N + 1)
    var primes: [Int] = []

    for i in 2..<isPrime.count {
        if isPrime[i] {
            primes.append(i)

            var idx = i + i
            while idx < isPrime.count {
                isPrime[idx] = false
                idx += i
            }
        }
    }

    var semiPrimes: [Int] = .init(repeating: 0, count: N+1)

    for prime1 in primes {
        for prime2 in primes {
            if prime1 * prime2 > N {
                break
            }
            semiPrimes[prime1 * prime2] = 1
        }
    }

    for i in 1..<semiPrimes.count {
        semiPrimes[i] += semiPrimes[i-1]
    }
    
    var answer: [Int] = []
    zip(P, Q).forEach { start, end in
        answer.append(semiPrimes[end] - semiPrimes[start-1])
    }

    return answer
}
```

## 코드 설명
O(N * log(log(N)) + M) 시간복잡도로 문제 해결

엄청나게 복잡했다.

우선 에라스토테네스의 체로 소수를 구했다.
그 뒤 모든 소수를 곱하여 SemiPrime을 구한 뒤 (SemiPrime의 범위도 N을 넘지 못하고, P, Q의 최대값도 N을 안넘는다.)

누적합 계산을 통하여 문제 해결.