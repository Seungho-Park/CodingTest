# Nesting

## 문제 설명
A string S consisting of N characters is called properly nested if:

- S is empty;
- S has the form "(U)" where U is a properly nested string;
- S has the form "VW" where V and W are properly nested strings.
- For example, string "(()(())())" is properly nested but string "())" isn't.

Write a function:

    public func solution(_ S : inout String) -> Int

that, given a string S consisting of N characters, returns 1 if string S is properly nested and 0 otherwise.

For example, given S = "(()(())())", the function should return 1 and given S = "())", the function should return 0, as explained above.

## 제한사항
 - N is an integer within the range [0..1,000,000];
 - string S is made only of the characters '(' and/or ')'.

## 입출력 예
| S | result |
| - | ------ |
|"(()(())())"|1|
|"())"|0|

## 소스 코드
```Swift
import Foundation
import Glibc

// you can write to stdout for debugging purposes, e.g.
// print("this is a debug message")

public func solution(_ S : inout String) -> Int {
    // Implement your solution here
    var stack: [Character] = []
    for value in S {
        if value == "(" {
            stack.append(value)
        } else if let last = stack.last, "\(last)\(value)" == "()" {
            stack.removeLast()
        } else {
            return 0
        }
    }

    return stack.isEmpty ? 1 : 0
}
```

## 코드 설명
시간복잡도 O(N)

Lesson 7 첫번째 문제인 Brackets의 하위버전?

같은 내용인 거 같은데 뭐가 다른건진 모르겠다.

문자열을 처음부터 돌면서 올바른 괄호로 이루어진 문자인지 Stack을 이용해서 확인했다.
