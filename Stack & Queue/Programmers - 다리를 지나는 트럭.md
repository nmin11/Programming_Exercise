## **Programmers > 스택/큐 > 다리를 지나는 트럭**

</br>

[연습 문제 링크](https://programmers.co.kr/learn/courses/30/lessons/42583)

</br>

📚 내가 사용한 프로그래밍 언어 : Java  
🎢 난이도 : Level 2

</br>

## 문제 요약

트럭 여러 대가 강을 가로지르는 일차선 다리를 정해진 순으로 건너려 한다.  
모든 트럭이 다리를 건너려면 최소 몇 초가 걸리는지 구해야 한다.  
다리에는 트럭이 최대 bridge_length대 올라갈 수 있으며, 다리는 weight 이하까지 무게를 견딜 수 있다.  
그리고 트럭들은 bridge_length만큼 앞으로 이동해야 다리를 완전히 통과할 수 있다.  
트럭 별 무게 truck_weights가 함께 주어졌을 때, 모든 트럭이 다리를 건너는 데 최소 몇 초가 걸리는지를 리턴하라.

</br>

## 추가 사항

- 1 <= bridge_length <= 10,000
- 1 <= weight <= 10,000
- 1 <= truck_weights.length <= 10,000
- 1 <= truck_weights[i] <= weight

</br>

## 내 풀이 (Java)

```java
import java.util.ArrayList;
import java.util.LinkedList;
import java.util.Queue;

class Solution {
    public int solution(int bridge_length, int weight, int[] truck_weights) {
        ArrayList<Integer> trucks = new ArrayList<>();
        Queue<Integer> q = new LinkedList<>();
        for (int i = 0; i < truck_weights.length; i++) {
            trucks.add(truck_weights[i]);
        }
        for (int i = 0; i < bridge_length; i++) {
            q.offer(0);
        }

        int count = 0;
        int total_weight = 0;
        while (!q.isEmpty()) {
            total_weight -= q.poll();
            count++;

            if (trucks.size() > 0) {
                if (total_weight + trucks.get(0) <= weight) {
                    total_weight += trucks.get(0);
                    q.offer(trucks.remove(0));
                } else {
                    q.offer(0);
                }
            }
        }

        return count;
    }
}
```

뭐 별 일 아니라고 생각할 수 있겠지만, 드디어 Java로, 그리고 온전히 내 힘으로 문제를 풀어낼 수 있었다. 👏  
하지만 여전히 Queue의 메소드들 중 offer나 add의 차이가 명확히 머릿속에 자리잡은 느낌은 아니라서 역시 연습은 더 필요할 것이다.  
그리고 문제를 풀면서도 자꾸 무의식적으로 JavaScript 풀듯이 풀고 있는 나 자신을 발견할 수 있었다. (이를테면 배열을 shift해서 첫번째 값을 지우면서 동시에 q에 넣으려고 한다던가...)  
확실히 Java로 도전했고 풀어냈다는 사실은 기념비적이지만 결코 연습을 게을리 하지 않도록 하자.

</br>

풀이는 무척 간단하다.  
일단 배열을 복사한 ArrayList와 다리의 길이만큼의 Queue를 준비한다.  
그 다음 queue의 요소를 하나씩 빼주고 시간을 재면서, 복사한 배열이 남아있으면 0이 되었든 복사한 배열의 0번째 값이 되었든 queue에 넣어준다.  
그 외의 경우라면 queue의 size는 계속해서 줄어들 것이고 결국 원하는 count 값을 도출해낼 것이다.

</br>

## 다른 사람의 풀이 (JavaScript)

```javascript
function solution(bridge_length, weight, truck_weights) {
  // '다리'를 모방한 큐에 간단한 배열로 정리 : [트럭무게, 얘가 나갈 시간].
  let time = 0,
    qu = [[0, 0]],
    weightOnBridge = 0;

  // 대기 트럭, 다리를 건너는 트럭이 모두 0일 때 까지 다음 루프 반복
  while (qu.length > 0 || truck_weights.length > 0) {
    // 1. 현재 시간이, 큐 맨 앞의 차의 '나갈 시간'과 같다면 내보내주고,
    //    다리 위 트럭 무게 합에서 빼준다.
    if (qu[0][1] === time) weightOnBridge -= qu.shift()[0];

    if (weightOnBridge + truck_weights[0] <= weight) {
      // 2. 다리 위 트럭 무게 합 + 대기중인 트럭의 첫 무게가 감당 무게 이하면
      //    다리 위 트럭 무게 업데이트, 큐 뒤에 [트럭무게, 이 트럭이 나갈 시간] 추가.
      weightOnBridge += truck_weights[0];
      qu.push([truck_weights.shift(), time + bridge_length]);
    } else {
      // 3. 다음 트럭이 못올라오는 상황이면 얼른 큐의
      //    첫번째 트럭이 빠지도록 그 시간으로 점프한다.
      //    참고: if 밖에서 1 더하기 때문에 -1 해줌
      if (qu[0]) time = qu[0][1] - 1;
    }
    // 시간 업데이트 해준다.
    time++;
  }
  return time;
}
```
