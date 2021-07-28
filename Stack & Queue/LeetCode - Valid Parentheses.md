bb## **LeetCode > Stack > Valid Parentheses**

</br>

[연습 문제 링크](https://leetcode.com/problems/valid-parentheses/)

</br>

:books: 내가 사용한 프로그래밍 언어 : Java  
:roller_coaster: 난이도 : Easy

</br>

## 영어 지문

Given a string s containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

An input string is valid if:

1. Open brackets must be closed by the same type of brackets.
2. Open brackets must be closed in the correct order.

</br>

(이 파일을 볼 때마다 영어 독해 능력을 조금이나마 늘리기 위해서 영어 지문을 복사해왔다.)

</br>

## 문제 요약

주어진 문자열 s는 소괄호, 중괄호, 대괄호의 열고 닫는 문자들을 포함한다.  
열린 브라켓이 같은 타입으로 닫혀있어야 하며, 열린 브라켓은 반드시 닫혀야 한다.  
검증 결과를 Boolean 타입으로 반환해라.

</br>

## 추가 사항

- 1 <= s.length <= 10⁴
- s consists of parentheses only '()[]{}'.

</br>

## 승지니어 님의 풀이

이 파일을 적은 2021년 7월 28일부터, 승지니어 님의 [기술면접 라이브코딩]을 통해 Algorithm을 학습해보려고 한다.  
Stack의 대표적인 문제라고 해서 오늘은 이 문제를 공부해보았다.  
아래의 풀이는 [승지니어 님의 풀이](https://www.youtube.com/watch?v=zeFkwKRG06Y&t=8s&ab_channel=%EC%8A%B9%EC%A7%80%EB%8B%88%EC%96%B4Sengineer) 를 참고한 것이다.

```java
class Solution {
    public boolean isValid(String s) {
        Stack<Character> stack = new Stack<>();
        char[] arr = s.toCharArray();
        for (char c : arr) {
            if (c == '(' || c == '{' || c == '[') {
                stack.push(c);
            } else if (c == ')') {
                if (stack.size() == 0 || stack.pop() != '(') {
                    return false;
                }
            } else if (c == '}') {
                if (stack.size() == 0 || stack.pop() != '{') {
                    return false;
                }
            } else if (c == ']') {
                if (stack.size() == 0 || stack.pop() != '[') {
                    return false;
                }
            } else {
                return false;
            }
        }
        return stack.size() == 0;
    }
}
```

문제가 간단했다고는 하지만 솔직히 내가 이러한 풀이를 도출해내려면 시간이 꽤나 소모되었으리라 예상된다.  
그런 만큼 이런 Stack의 간단한 활용 예시를 꼭! 유념해두도록 하자.
