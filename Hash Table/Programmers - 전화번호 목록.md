## **Programmers > 해시 > 전화번호 목록**

</br>

[연습 문제 링크](https://programmers.co.kr/learn/courses/30/lessons/42577)

</br>

📚 내가 사용한 프로그래밍 언어 : Java  
🎢 난이도 : Level 2

</br>

## 문제 요약

전화번호부에 적힌 전화번호 중, 한 번호가 다른 번호의 접두어인 경우가 있는지 확인하려고 한다.  
전화번호가 다음과 같을 경우, 구조대 전화번호는 영석이의 전화번호의 접두사이다.

- 구조대 : 119
- 박준영 : 97674223
- 지영석 : 1195524421

전화번호부에 적힌 전화번호를 담은 배열 phone_book이 매개변수로 주어질 때, 어떤 번호가 다른 번호의 접두어인 경우가 있으면 false를, 그렇지 않으면 true를 리턴하라.

</br>

## 추가 사항

- 1 <= phone_book.length <= 1,000,000
- 각 전화번호의 길이는 1 이상 20 이하
- 전화번호는 중복되지 않음

</br>

## 다른 사람의 풀이

```java
import java.util.HashMap;

class Solution {
    public boolean solution(String[] phone_book) {
        boolean answer = true;

        HashMap<String, Integer> map = new HashMap<>();
        for (int i = 0; i < phone_book.length; i++) {
            map.put(phone_book[i], i);
        }
        for (int i = 0; i < phone_book.length; i++) {
            for (int j = 1; j < phone_book[i].length(); j++) {
                if (map.containsKey(phone_book[i].substring(0, j))) {
                    answer = false;
                    return answer;
                }
            }
        }

        return answer;
    }
}
```

문제를 딱 보고 몇 분 이내에 다른 사람의 풀이를 보기로 했다.  
문제는 간단해보이지만 내가 놓치고 있는 개념적인 어떤 부분이 있을 것이라 확신했기 때문이다. ~~자랑이다~~  
아니나 다를까, HashMap을 활용한 문제풀이는 내가 쉽게 도출해내지 못했을 법한 것이었다.  
Stack, Queue와 더불어 문제풀이에 요긴하게 쓸 수 있는 친구이니 꼭 메소드들을 기억해두고 잘 활용할 수 있도록 하자.  
우선, 이 풀이에서 사용된 containsKey()는 메소드의 인자값을 key값으로 가지는 map 요소가 있는지를 boolean 타입으로 반환해주는 메소드이다.  
이를 반복문으로 돌리면서 접두어를 간단하게 찾아내었다.
