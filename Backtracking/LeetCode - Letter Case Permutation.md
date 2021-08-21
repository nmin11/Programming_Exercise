## **LeetCode > String / Backtracking / Bit Manipulation > Letter Case Permutation**

</br>

[연습 문제 링크](https://leetcode.com/problems/sudoku-solver/)

</br>

📚 내가 사용한 프로그래밍 언어 : Java  
🎢 난이도 : Medium

</br>

## 영어 지문

Given a string s, we can transform every letter individually to be lowercase or uppercase to create another string.  
Return _a list of all possible strings we could create_. You can return the output in **any order**.

</br>

## 추가 사항

- 1 <= s.length <= 12
- s will consist only of letters or digits.

</br>

## 문제 요약

문자열 s가 주어진다.  
우리는 모든 알파벳을 개별적으로 소문자나 대문자로 바꿔서 새로운 문자열을 만들 수 있다.  
가능한 모든 문자열들을 담은 배열을 반환하라.  
반환할 output의 배열은 순서가 어떻게 되어 있어도 상관 없다.

</br>

## [승지니어 님의 풀이](https://www.youtube.com/watch?v=tc0CKG0faZU&ab_channel=%EC%8A%B9%EC%A7%80%EB%8B%88%EC%96%B4Sengineer)

```java
/*
백트래킹 :
조건에 맞는 모든 경우를 찾고 싶을 때,
조건에 맞는 값을 찾을 때까지 전진
더이상 나갈 길이 없으면 한칸 후퇴
이를 계속해서 반복

결국엔 재귀 구현
*/
class Solution {
    public List<String> letterCasePermutation(String s) {
        char[] arr = s.toCharArray();
        List<String> result = new ArrayList<>();
        backtrack(arr, result, 0);
        return result;
    }

    public void backtrack(char[] arr, List<String> result, int idx) {
        if (idx == arr.length) {
            //종료 조건
            result.add(new String(arr));
        } else {
            char c = arr[idx];
            if (isAlpha(c)) {
                arr[idx] = Character.toLowerCase(c);
                backtrack(arr, result, idx + 1);
                arr[idx] = Character.toUpperCase(c);
                backtrack(arr, result, idx + 1);
            } else {
                backtrack(arr, result, idx + 1);
            }
        }
    }

    public boolean isAlpha(char c) {
        return (c >= 'a' && c <= 'z') || (c>='A' && c <= 'Z');
    }
}
```

character 배열에 문자열을 담아서 for문을 통해 모든 문자마다 소문자 및 대문자 변환을 시도하고 backtrack을 재귀 호출한다.

</br>

backtracking은 결국엔 재귀를 구현한다고는 하는데, 사실 코드의 흐름이 쉽게 이해가 되지 않는다.  
아직도 재귀에 대한 이해도 자체가 많이 낮다는 생각도 든다.
