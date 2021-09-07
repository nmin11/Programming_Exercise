## **Programmers > Heap > 디스크 컨트롤러**

</br>

[연습 문제 링크](https://programmers.co.kr/learn/courses/30/lessons/42627)

</br>

📚 내가 사용한 프로그래밍 언어 : Java  
🎢 난이도 : Level 3

</br>

## 문제 요약

하드디스크는 한 번에 하나의 작업만 수행할 수 있다.  
디스크 컨트롤러를 구현하는 방법은 여러 가지가 있다.  
가장 일반적인 방법은 요청이 들어온 순서대로 처리하는 것이다.

```
0ms 시점에 3ms가 소요되는 A작업 요청
1ms 시점에 9ms가 소요되는 B작업 요청
2ms 시점에 6ms가 소요되는 C작업 요청
```

요청이 이렇게 들어왔을 때 순서대로 처리하면 다음과 같다.

</br>

<img width="628" alt="디스크 순서대로 처리" src="https://user-images.githubusercontent.com/75058239/132218836-5699c835-da9e-441e-86a1-da7fc23c5297.png">

</br>

한 번에 하나의 요청만 수행할 수 있기 때문에 처리 방식은 다음과 같이 진행된다.

```
A: 3ms 시점에 작업 완료 (요청에서 종료까지 : 3ms)
B: 1ms부터 대기하다가, 3ms 시점에 작업을 시작해서 12ms 시점에 작업 완료(요청에서 종료까지 : 11ms)
C: 2ms부터 대기하다가, 12ms 시점에 작업을 시작해서 18ms 시점에 작업 완료(요청에서 종료까지 : 16ms)
```

이 때 각 작업의 요청부터 종료까지 걸린 시간의 평균은 10ms가 된다.  
하지만 A → C → B 순서대로 처리하면

</br>

<img width="676" alt="디스크 효율적인 처리" src="https://user-images.githubusercontent.com/75058239/132218853-9c4a685c-36ff-4f05-bb8f-986f127a4415.png">

</br>

```
A: 3ms 시점에 작업 완료(요청에서 종료까지 : 3ms)
C: 2ms부터 대기하다가, 3ms 시점에 작업을 시작해서 9ms 시점에 작업 완료(요청에서 종료까지 : 7ms)
B: 1ms부터 대기하다가, 9ms 시점에 작업을 시작해서 18ms 시점에 작업 완료(요청에서 종료까지 : 17ms)
```

이렇게 하면 각 작업의 요청부터 종료까지 걸린 시간의 평균은 9ms가 된다.

</br>

각 작업에 대해 [작업 요청 시점, 작업 소요시간]을 담은 2차원 배열 jobs가 매개변수로 주어질 때, 작업의 요청부터 종료까지 걸린 시간의 평균을 가장 줄이는 방법으로 처리하면 평균이 얼마가 되는지 리턴하라.  
(단 소수점 이하의 수는 버린다.)

</br>

## 추가 사항

- 1 <= jobs.length <= 500
- 작업 요청 시점과 작업 소요시간은 0 이상 1,000 이하

</br>

## 다른 사람의 풀이 (Java)

```java
import java.util.Arrays;
import java.util.PriorityQueue;

class Solution {
    public int solution(int[][] jobs) {
        int answer = 0;
        int end = 0;
        int jobsIdx = 0;
        int count = 0;

        Arrays.sort(jobs, (a, b) -> a[0] - b[0]);
        PriorityQueue<int[]> pq = new PriorityQueue<>((a, b) -> a[1] - b[1]);

        while (count < jobs.length) {
            while (jobsIdx < jobs.length && jobs[jobsIdx][0] <= end) {
                pq.add(jobs[jobsIdx++]);
            }

            if (pq.isEmpty()) {
                end = jobs[jobsIdx][0];
            } else {
                int[] tmp = pq.poll();
                answer += tmp[1] + end - tmp[0];
                end += tmp[1];
                count++;
            }
        }
        return answer / jobs.length;
    }
}
```

상당히 오랜 시간 고민하고 시도해보면서 문제에 접근해보았지만 풀어내지 못했다.  
사실 고집불통으로 좀 더 풀어보고도 싶었지만 투자한 시간이 너무나도 길었기에, 다른 사람의 풀이를 참조하게 되었다.  
자존심이 많이 꺾였지만 낙담하지 말고 좋은 풀이 방식을 익히는 데에 집중하자.
