## **Programmers > 해시 > 위장**

</br>

[연습 문제 링크](https://programmers.co.kr/learn/courses/30/lessons/42578)

</br>

📚 내가 사용한 프로그래밍 언어 : Java  
🎢 난이도 : Level 2

</br>

## 문제 요약

스파이들은 매일 다른 옷을 조합해서 자신을 위장한다.  
스파이가 가진 의상들이 담긴 2차원 배열 clothes가 주어질 때 서로 다른 옷의 조합의 수를 리턴하라.

</br>

## 추가 사항

- clothes[i] = [의상의 이름, 의상의 종류]
- 스파이가 가진 의상의 총 갯수는 1개 이상 30개 이하
- 같은 이름의 의상은 없음
- 스파이는 하루에 최소 한개의 의상을 입음

</br>

## 다른 사람의 풀이 (Java)

```java
import java.util.HashMap;
import java.util.Iterator;

class Solution {
    public int solution(String[][] clothes) {
        int answer = 1;

        HashMap<String, Integer> map = new HashMap<>();
        for (String[] el : clothes) {
            if (map.containsKey(el[1])) {
                map.put(el[1], map.get(el[1]) + 1);
            } else {
                map.put(el[1], 1);
            }
        }

        Iterator<Integer> it = map.values().iterator();
        while (it.hasNext()) {
            answer *= it.next().intValue() + 1;
        }

        return answer - 1;
    }
}
```

부끄럽게도 직접 풀어내지 못했다.  
두세 시간은 고민한 것 같은데, HashMap은 어떻게 활용한다 쳐도 조합의 총 갯수를 떠올리기가 쉽지 않았다.  
하지만 해법은 허무하리만치 간단했다.  
(각 의상의 종류별 의상의 갯수 + 1)을 모든 종류만큼 곱해준다.  
그 이후, 마지막에 1을 빼주기만 하면 답이 도출된다.  
마지막에 1을 빼주는 이유는 아무 것도 입지 않았을 경우를 빼주는 것이다.  
정말 너무 힘이 빠지는 느낌···.
