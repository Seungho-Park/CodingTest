# GenomicRangeQuery

## 문제 설명
A DNA sequence can be represented as a string consisting of the letters A, C, G and T, which correspond to the types of successive nucleotides in the sequence. Each nucleotide has an impact factor, which is an integer. Nucleotides of types A, C, G and T have impact factors of 1, 2, 3 and 4, respectively. You are going to answer several queries of the form: What is the minimal impact factor of nucleotides contained in a particular part of the given DNA sequence?

The DNA sequence is given as a non-empty string S = S[0]S[1]...S[N-1] consisting of N characters. There are M queries, which are given in non-empty arrays P and Q, each consisting of M integers. The K-th query (0 ≤ K < M) requires you to find the minimal impact factor of nucleotides contained in the DNA sequence between positions P[K] and Q[K] (inclusive).

For example, consider string S = CAGCCTA and arrays P, Q such that:

    P[0] = 2    Q[0] = 4
    P[1] = 5    Q[1] = 5
    P[2] = 0    Q[2] = 6
The answers to these M = 3 queries are as follows:

The part of the DNA between positions 2 and 4 contains nucleotides G and C (twice), whose impact factors are 3 and 2 respectively, so the answer is 2.
The part between positions 5 and 5 contains a single nucleotide T, whose impact factor is 4, so the answer is 4.
The part between positions 0 and 6 (the whole string) contains all nucleotides, in particular nucleotide A whose impact factor is 1, so the answer is 1.
Write a function:

    public func solution(_ S : inout String, _ P : inout [Int], _ Q : inout [Int]) -> [Int]

that, given a non-empty string S consisting of N characters and two non-empty arrays P and Q consisting of M integers, returns an array consisting of M integers specifying the consecutive answers to all queries.

Result array should be returned as an array of integers.

## 제한사항
 - N is an integer within the range [1..100,000];
 - M is an integer within the range [1..50,000];
 - each element of arrays P and Q is an integer within the range [0..N - 1];
 - P[K] ≤ Q[K], where 0 ≤ K < M;
 - string S consists only of upper-case English letters A, C, G, T.

## 입출력 예
|S|P|Q|result|
|-|-|-|------|
|CAGCCTA|[2,5,0]|[4,5,6]|[2,4,1]|


## 소스 코드
```Swift
import Foundation
import Glibc

// you can write to stdout for debugging purposes, e.g.
// print("this is a debug message")

public func solution(_ S : inout String, _ P : inout [Int], _ Q : inout [Int]) -> [Int] {
    // Implement your solution here
    var array: [[Int]] = .init(repeating: .init(repeating: 0, count: S.count+1), count: 3)

    var idx = 1
    for value in S {
        array[0][idx] = array[0][idx-1]
        array[1][idx] = array[1][idx-1]
        array[2][idx] = array[2][idx-1]

        switch value {
            case "A": array[0][idx] += 1
            case "C": array[1][idx] += 1
            case "G": array[2][idx] += 1
            default: break
        }

        idx += 1
    }

    var answer: [Int] = []
    zip(P, Q).forEach {
        if array[0][$1+1] - array[0][$0] > 0 {
            answer.append(1)
        } else if array[1][$1+1] - array[1][$0] > 0 {
            answer.append(2)
        } else if array[2][$1+1] - array[2][$0] > 0 {
            answer.append(3)
        } else {
            answer.append(4)
        }
    }

    return answer
}
```

## 코드 설명
문제 자체는 어렵지 않으나, 알고리즘(푸는 방법)을 모른다면 시간복잡도를 절대 통과할 수 없는 가장 까다로운 문제였다.

설명하는 것도 어려운데, 
1. A, C, G가 등장했는지 확인할 배열을 만든다. (capacity: S+1)
2. 0번 인덱스는 처음 등장한 문자인지 확인하기 위해 비워둔다
3. S를 돌며 해당 문자열이 등장했다면 해당 배열을 이전배열값 + 1 해준다.
4. P, Q를 돌며 A ~ G까지 (ex: A[Q+1] - A[P] > 0) 이면 해당 문자가 등장한 것이므로 해당 인덱스를 정답 배열에 추가
5. A~G까지 돌았는데 해당하는 게 없으면 T가 등장한 것이므로 4를 추가해준다.

끝.

시간복잡도는 O(N+M)으로 통과하였다.