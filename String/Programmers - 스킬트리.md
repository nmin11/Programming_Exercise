## **Programmers > Summer/Winter Coding(~2018) > 스킬트리**

</br>

[연습 문제 링크](https://programmers.co.kr/learn/courses/30/lessons/49993)

</br>

:books: 내가 사용한 프로그래밍 언어 : Java  
:roller_coaster: 난이도 : Level 2

</br>

## 문제 요약

게임을 플레이하는 유저들이 본인이 원하는 스킬트리에 따라 스킬을 찍고자 한다.  
하지만 찍고자 하는 스킬에 선행 스킬이 있다면 반드시 선행 스킬을 먼저 찍고 나서 원하는 스킬을 찍을 수 있다.  
선행 스킬 순서에 없는 나머지 스킬들은 순서에 상관 없이 배울 수 있다.  
선행 스킬 순서 skill과 유저들이 만든 스킬트리를 담은 배열 skill_trees가 매개 변수로 주어질 때, 가능한 스킬트리 개수를 리턴하라.

</br>

## 추가 사항

- 각 스킬들은 알파벳 대문자로 표기하며, 모든 문자열은 알파벳 대문자로만 이루어져 있음
- 선행 스킬 순서와 유저들이 찍고자 하는 스킬트리는 문자열로 표기함
  - 예를 들어 C → B → D 라면 "CBD"로 표기
- 1 <= skill <= 26, skill은 중복해서 주어지지 않음
- 1 <= skill_trees.length <= 20
- skill_trees[i]는 i번째 유저가 찍고자 하는 스킬트리를 나타내는 문자열
  - 2 <= skill_trees[i].length <= 26, 중복되는 알파벳 대문자는 없음

</br>

## 내 풀이

```java
import java.util.Stack;

class Solution {
    public int solution(String skill, String[] skill_trees) {
        int answer = 0;

        Stack<Character> stack = new Stack<>();
        char[] arr = skill.toCharArray();
        boolean flag;

        for (int i = 0; i < skill_trees.length; i++) {
            flag = true;
            stack.clear();

            for (int j = 0; j < skill_trees[i].length(); j++) {
                for (int k = 0; k < arr.length; k++) {
                    if (skill_trees[i].charAt(j) == arr[k]) {
                        if (stack.empty()) {
                            if (k == 0) stack.push(arr[k]);
                            else flag = false;
                        } else {
                            if (k != 0) {
                                if (stack.peek() == arr[k - 1]) {
                                    stack.push(arr[k]);
                                } else flag = false;
                            }
                        }
                    }
                }
            }

            if (flag) answer++;
        }
        return answer;
    }
}
```

이전에 살펴보았던 [Valid Parentheses](https://github.com/nmin11/Programming_Exercise/blob/main/Stack%20%26%20Queue/LeetCode%20-%20Valid%20Parentheses.md) 문제가 떠올라서 Stack을 활용해서 문제를 풀어보기로 했다.  
for문을 무려 3중으로 사용하는 과정이기 때문에 시간 복잡도가 엄청난 로직이다.  
하지만 고집 불통으로 밀어붙여서 Stack을 통해 원하는 답을 도출해낼 수 있었다.

</br>

풀이를 살펴보자면 우선 각 유저들이 원하는 스킬트리 문자열을 하나하나 꺼내보면서 선행 스킬 순서인 skill의 요소와 겹치는 것이 있는지 확인한다.  
있을 경우에 한해서 다시 Stack이 비어있는 경우와 그렇지 않은 경우로 나눈다.  
비어 있는 경우 해당 스킬이 선행 스킬 순서의 첫번째 스킬이면 Stack에 넣어주고 아니라면 유효하지 못한것으로 판명한다.  
Stack이 비어있지 않은 경우, 이전 Stack 값을 꺼내서 해당 값이 순서에 맞는지를 확인하면서 유효성을 검증한다.

</br>

## 다른 사람의 풀이

```java
import java.util.*;

class Solution {
    public int solution(String skill, String[] skill_trees) {
        int answer = 0;
        ArrayList<String> skillTrees = new ArrayList<String>(Arrays.asList(skill_trees));
        Iterator<String> it = skillTrees.iterator();

        while (it.hasNext()) {
            if (skill.indexOf(it.next().replaceAll("[^" + skill + "]", "")) != 0) {
                it.remove();
            }
        }
        answer = skillTrees.size();
        return answer;
    }
}
```

나와는 아예 다른 방법으로 문제에 접근했음을 확인할 수 있었다.  
그리고 아마도 이러한 방법이 출제자의 의도가 아니었을지 생각해볼 수 있었다.  
정규표현식의 활용과 Iterator에 대해서 조금 더 공부를 해봐야겠다.
