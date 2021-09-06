## **Programmers > Heap > 더 맵게**

</br>

[연습 문제 링크](https://programmers.co.kr/learn/courses/30/lessons/42626)

</br>

📚 내가 사용한 프로그래밍 언어 : Java  
🎢 난이도 : Level 2

</br>

## 문제 요약

매운 것을 좋아하는 Leo는 모든 음식의 스코빌 지수를 K 이상으로 만들고 싶다.  
모든 음식의 스코빌 지수를 K 이상으로 만들기 위해 Leo는 스코빌 지수가 가장 낮은 두 개의 음식을 아래와 같은 방법으로 섞어서 새로운 음식을 만든다.

```
섞은 음식 스코빌 지수 = 가장 안 매운 음식 스코빌 지수 + (두번째로 안 매운 음식 스코빌 지수 * 2)
```

Leo는 모든 음식의 스코빌 지수가 K 이상이 될 때까지 반복해서 섞는다.  
Leo가 가진 음식의 스코빌 지수를 담은 배열 scoville과 원하는 스코빌 지수가 K가 주어질 때, 모든 음식의 스코빌 지수를 K 이상으로 만들기 위한 최소 횟수를 리턴하라.

</br>

## 추가 사항

- 2 <= scoville.length <= 1,000,000
- 0 <= K <= 1,000,000,000
- 0 <= scoville[i] <= 1,000,000
- **모든 음식의 스코빌 지수를 K 이상으로 만들 수 없는 경우 -1을 리턴**

</br>

## 내 첫 풀이 (오답) (Java)

```java
import java.util.PriorityQueue;

class Solution {
    public int solution(int[] scoville, int K) {
        PriorityQueue<Integer> pq = new PriorityQueue<>();
        for (int el : scoville) {
            if (el < K) {
                pq.add(el);
            }
        }

        int count = 0;
        while (!pq.isEmpty()) {
            int target = pq.poll();
            if (pq.peek() != null) {
                target += (pq.poll() * 2);
                if (target < K) {
                    pq.add(target);
                }
                count++;
            } else {
                return -1;
            }
        }

        return count;
    }
}
```

테스트 케이스 6, 7, 10, 13번을 실패했다.  
'질문하기' 탭을 몇십분 정도 들여다보고, 그 원인을 파악할 수 있었다.  
원인은 바로, 내 우선순위 큐는 처음에 K보다 작은 값들만 넣어서 다루기로 했기 때문에, 만약에 내 우선순위 큐에 가장 작은 값 하나만 남았을 때, 두번째로 작은 값은 K 이상인 값들 중에서도 골라올 수 있어야 한다는 점이었다.

</br>

## 내 풀이 (Java)

```java
import java.util.PriorityQueue;

class Solution {
    public int solution(int[] scoville, int K) {
        PriorityQueue<Integer> pq = new PriorityQueue<>();
        PriorityQueue<Integer> remain = new PriorityQueue<>();
        for (int el : scoville) {
            if (el < K) {
                pq.add(el);
            } else {
                remain.add(el);
            }
        }

        int count = 0;
        while (!pq.isEmpty()) {
            int target = pq.poll();
            if (pq.peek() != null) {
                target += (pq.poll() * 2);
                if (target < K) {
                    pq.add(target);
                } else {
                    remain.add(target);
                }
                count++;
            } else {
                if (!remain.isEmpty() && target + (remain.peek() * 2) >= K) {
                    target += remain.poll() * 2;
                    remain.add(target);
                    count++;
                } else {
                    return -1;
                }
            }
        }

        return count;
    }
}
```

우선순위 큐를 하나 더 선언해서 스코빌 지수가 K 이상인 음식들을 넣어주었다.  
이에 따라 while 문 안에서도 또다른 우선순위 큐에 대한 로직들을 추가해주어야만 했다.  
본 문제에는 효율성 테스트도 있고 했지만 이렇게 해도 테스트에는 모두 통과하는 모습을 확인할 수 있었다.  
하지만 우선순위 큐를 2개나 쓴다는 사실이 못 미덥긴 하다.

</br>

## 다른 사람의 풀이 (Java)

```java
import java.util.*;
class Solution {
    public int solution(int[] scoville, int K) {
        PriorityQueue<Integer> q = new PriorityQueue<>();

        for(int i = 0; i < scoville.length; i++)
            q.add(scoville[i]);

        int count = 0;
        while(q.size() > 1 && q.peek() < K){
            int weakHot = q.poll();
            int secondWeakHot = q.poll();

            int mixHot = weakHot + (secondWeakHot * 2);
            q.add(mixHot);
            count++;
        }

        if(q.size() <= 1 && q.peek() < K)
            count = -1;

        return count;
    }
}
```

내가 쓸데없이 복잡다단하게 접근했다는 점을 확인할 수 있었다.  
아무래도 나는 조건을 섬세하게 걸어주는 작업에 약한 것 같다.  
로직이 비슷하다고 하여 대강 보고 넘어갈 것이 아니라, 이런 깔끔한 설계 방식을 직접 활용할 수 있을 만큼 보고 연습하자.
