## **Programmers > Greedy > 구명보트**

</br>

[연습 문제 링크](https://programmers.co.kr/learn/courses/30/lessons/42885)

</br>

📚 내가 사용한 프로그래밍 언어 : Java, JavaScript  
🎢 난이도 : Level 2

</br>

## 문제 요약

무인도에 갇힌 사람들을 구명보트를 이용해서 구출하려 한다.  
구명보트는 작아서 **최대 2명** 탈 수 있으며, 무게 제한도 있다.  
예를 들어, 사람들의 몸무게가 [70kg, 50kg, 80kg, 50kg]이고 구명보트의 무게 제한이 100kg이라면 2번째 사람과 4번째 사람은 같이 탈 수 있지만 1번째 사람과 3번째 사람은 같이 탈 수 없다.  
구명보트를 최대한 적게 사용하여 모든 사람을 구출하려고 한다.  
사람들의 몸무게를 담은 배열 `people`과 구명보트의 무게제한 `limit`가 매개변수로 주어질 때, 모든 사람을 구출하기 위해 필요한 구명보트 개수의 최소값을 리턴하라.

</br>

## 추가 사항

- 1 <= people.length <= 50,000
- 40 <= people[i] <= 240
- 40 <= limit <= 240
- limit는 항상 사람들의 몸무게 중 최대값보다 크게 주어지므로 사람들을 구출할 수 없는 경우는 없음

</br>

## 내 풀이

```java
import java.util.Arrays;

class Solution {
    public int solution(int[] people, int limit) {
        Arrays.sort(people);
        int twoPeople = 0;
        int leftIdx = 0;
        int rightIdx = people.length - 1;

        while (leftIdx < rightIdx) {
            if (people[leftIdx] + people[rightIdx] <= limit) {
                leftIdx++;
                rightIdx--;
                twoPeople++;
            } else {
                rightIdx--;
            }
        }

        return people.length - twoPeople;
    }
}
```

우선, 사람들을 몸무게 순으로 오름차순 정렬한 뒤, 가장 가벼운 사람의 인덱스와 가장 무거운 사람의 인덱스를 변수로 저장해둔다.  
그리고 두 사람이 같이 이동한 횟수를 저장해두기 위한 변수를 따로 지정해둔다.

</br>

이후, 가벼운 사람의 인덱스와 무거운 사람의 인덱스가 만날 때까지 양쪽 끝의 값들을 더한 값을 limit와 비교하면서, 그 값이 limit 이내라면 같이 이동한 횟수를 늘려주면서 양쪽 인덱스를 좁혀준다.  
만약 양쪽 끝의 값을 더한 값이 limit 값을 넘어간다면, 가장 무거운 인덱스 하나만 보트에 태운 것으로 처리하여 오른쪽 인덱스만을 줄여준다.

</br>

마지막으로, 총원에서 두 사람이 같이 이동한 횟수를 빼주면 자연스럽게 필요한 보트의 최소 개수가 도출된다.

</br>

## 소감

코드스테이츠에서의 학습 과정 중에 풀어보았던 문제가 나와서 상당히 반가웠다.  
그 때 당시 아쉽게도 스스로의 힘으로 풀어내지 못하고 Reference를 확인했었는데, 이번 기회에 다시 풀어보면서 문제에 대해 확실히 이해하고 넘어갈 수 있게 되었다.
