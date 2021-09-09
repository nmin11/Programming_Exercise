## **Programmers > Heap > 이중우선순위큐**

</br>

[연습 문제 링크](https://programmers.co.kr/learn/courses/30/lessons/42628)

</br>

📚 내가 사용한 프로그래밍 언어 : Java  
🎢 난이도 : Level 3

</br>

## 문제 요약

이중 우선순위 큐는 다음 연산을 할 수 있는 자료구조를 말한다.

| 명령어 | 로직                    |
| :----: | :---------------------- |
| I 숫자 | 큐에 주어진 숫자를 삽입 |
|  D 1   | 큐에서 최댓값 삭제      |
|  D -1  | 큐에서 최솟값 삭제      |

이중 우선순위 큐가 처리할 연산 operations가 매개변수로 주어질 때, 모든 연산을 처리한 후 큐가 비어있으면 [0, 0]을, 비어있지 않으면 [최댓값, 최솟값]을 리턴하라.

</br>

## 추가 사항

- 1 <= operations.length <= 1,000,000
- 최댓값/최솟값을 삭제하는 연산에서 해당 값이 둘 이상이면 하나만 삭제
- 빈 큐에 데이터를 삭제하라는 연산이 주어질 경우, 해당 연산 무시

</br>

## 내 풀이 (Java)

```java
import java.util.ArrayList;
import java.util.PriorityQueue;
import java.util.Collections;

class Solution {
    public int[] solution(String[] operations) {
        PriorityQueue<Integer> ascending = new PriorityQueue<>();
        PriorityQueue<Integer> descending = new PriorityQueue<>(Collections.reverseOrder());
        ArrayList<Integer> reg = new ArrayList<>();

        for (int i = 0; i < operations.length; i++) {
            String[] str = operations[i].split(" ");

            if (str[0].equals("I")) {
                reg.add(Integer.parseInt(str[1]));
                ascending.add(Integer.parseInt(str[1]));
                descending.add(Integer.parseInt(str[1]));
            } else if (str[0].equals("D")) {
                if (reg.size() == 0) continue;

                if (str[1].equals("1")) {
                    reg.remove(Integer.valueOf(descending.peek()));

                } else if (str[1].equals("-1")) {
                    reg.remove(Integer.valueOf(ascending.peek()));
                }

                ascending.clear();
                descending.clear();
                for (int el : reg) {
                    ascending.add(el);
                    descending.add(el);
                }
            }
        }

        int[] answer = new int[2];

        if (reg.size() == 0) {
            answer[0] = 0;
            answer[1] = 0;
            return answer;
        }

        answer[0] = descending.peek();
        answer[1] = ascending.peek();

        return answer;
    }
}
```

## 내 로직

1. 최솟값을 뽑기 위한 우선순위 큐, 최댓값을 뽑기 위한 우선순위 큐, 중간 다리 역할을 해줄 ArrayList를 각각 선언해준다.
2. operations 배열을 loop하면서, 배열 안의 문자열들을 가지고 다시 배열로 나누어준다.
3. 그렇게 나눈 배열 `str`을 가지고, 첫번째 값이 "D"인지 "I"인지 확인한다.
4. 첫번째 방의 값이 "I"인 경우, 두번째 값의 정수 값을 선언한 3가지 타입에 모두 넣어준다.
5. 첫번째 방의 값이 "D"인 경우, 일단 size가 0이 아닌지 간단하게 확인하고, 두번째 방의 값이 "1"인지 "-1"인지에 따라 ArrayList의 값을 우선순위 큐에서 찾아내서 삭제한다.
6. 우선순위 큐 둘 다 모두 비워버리고 ArrayList의 값을 다시 채워 넣는다.
7. loop 이후, 다시 간단하게 값들의 size를 체크하고, 값이 남아있다면 우선순위 큐에서 최댓값, 최솟값을 하나씩 뽑아서 반환해준다.

내가 짜놓고도 생각하기에, 시간복잡도가 엄청나지 않을까, 하는 생각이 들었다.  
`추가 사항`을 보면 operations의 길이가 1,000,000 까지 갈 수도 있다고 하니, 어쩌면 통과를 못할 수도 있겠다는 생각이 들었다.  
하지만 놀랍게도 위 코드는 1ms 이내에 통과되는 모습을 보여주었다.  
내가 로직을 잘 짰다기보다도, 우선순위 큐의 힘이 발휘된 게 아닐까 싶다.

</br>

## 여담

그리고 사실, 이 문제는 프로그래머스의 Level 3 문제였기에, 나는 위 로직을 생각해내고도, '에이 설마 이 정도 로직으로 풀리지 않겠지' 하는 의심 반, 그래도 해보고 싶은 마음 반으로 위 코드를 짜냈다.  
그리고 놀랍게도 이런 간단한 로직으로도 풀리는 모습을 확인할 수 있었다.  
프로그래머스에서 제공하는 Heap(우선순위 큐) 중에서 이 문제의 바로 이전 문제가 엄청 까다롭게 느껴졌기에 이번에도 지레 겁을 먹었는데, 이렇게 간단하게 풀리니 뭔가 허무했다.  
이 문제는 Level 2 정도로 낮춰야되지 않나, 하는 생각도 든다.

</br>

## 다른 사람의 풀이 (Java)

```java
import java.util.Collections;
import java.util.PriorityQueue;

class Solution {
    public int[] solution(String[] arguments) {
        int[] answer = {0,0};

        PriorityQueue<Integer> pq = new PriorityQueue<Integer>();
        PriorityQueue<Integer> reverse_pq = new PriorityQueue<Integer>(Collections.reverseOrder());

        for(int i=0; i<arguments.length; i++) {
            String temp[] = arguments[i].split(" ");
            switch(temp[0]) {
            case "I" :
                pq.add(Integer.parseInt(temp[1]));
                reverse_pq.add(Integer.parseInt(temp[1]));
                break;
            case "D" :
                if(pq.size() > 0) {
                    if(Integer.parseInt(temp[1]) == 1) {
                        // 최댓값 삭제
                        int max = reverse_pq.poll();
                        pq.remove(max);
                    } else {
                        // 최솟값 삭제
                        int min = pq.poll();
                        reverse_pq.remove(min);
                    }
                }
                break;
            }
        }

        if(pq.size() >= 0) {
            answer[0] = reverse_pq.poll();
            answer[1] = pq.poll();
        }

        return answer;
    }
}
```

로직이 상당히 비슷하지만 나처럼 별도의 ArrayList를 선언하지 않아도 되었다는 점에서 더욱 효율적이다.  
**우선순위 큐에서 remove 메소드를 통해 원하는 값을 찾아내서 삭제할 수 있다는 점**을 처음 알았다.  
간단하게 기억만 해두고 넘어갈 게 아니라, 확실하게 기록해두고 남겨놓기 위해서 이렇게 옮겨 적었다.
