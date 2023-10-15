# Brackets

## 문제 설명
A string S consisting of N characters is considered to be properly nested if any of the following conditions is true:

- S is empty;
- S has the form "(U)" or "[U]" or "{U}" where U is a properly nested string;
- S has the form "VW" where V and W are properly nested strings.

For example, the string "{[()()]}" is properly nested but "([)()]" is not.

Write a function:

    public func solution(_ S : inout String) -> Int

that, given a string S consisting of N characters, returns 1 if S is properly nested and 0 otherwise.

## 제한사항
 - N is an integer within the range [0..200,000];
 - string S is made only of the following characters: '(', '{', '[', ']', '}' and/or ')'.

## 입출력 예
| S | result |
| - | ------ |
|"{[()()]}"|1|
|"([)()]"|0|

## 소스 코드
```Swift
import Foundation
import Glibc

// you can write to stdout for debugging purposes, e.g.
// print("this is a debug message")

public func solution(_ S : inout String) -> Int {
    // Implement your solution here
    var stack: [Character] = []

    for char in S {
        if char == "(" || char == "[" || char == "{" {
            stack.append(char)
        } else if let last = stack.last, (
            String("\(last)\(char)") == "[]" ||
            String("\(last)\(char)") == "()" ||
            String("\(last)\(char)") == "{}") {
            stack.removeLast()
        } else {
            return 0
        }
    }

    return stack.isEmpty ? 1 : 0
}
```

## 코드 설명
스택을 사용하여 푸는 간단한 문제였다.

1. 우선 괄호의 시작('(', '{', '[')이 나온다면 스택에 집어넣고
괄호의 끝이 나온다면 스택에서 마지막을 꺼내 올바른 괄호가 만들어지는지 확인한다.

2. 올바른 괄호가 맞다면 스택의 마지막을 지우고 다시 1번부터 반복
3. 올바른 괄호가 만들어지지 않는다면 0을 반환
4. 모든 과정이 끝났다면 Stack이 비어있는지 확인하여 전부 올바른 괄호였는지 확인 후 1을 반환, 아니라면 0을 반환한다.

시간복잡도는 O(N)