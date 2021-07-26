## **Programmers > 2019 KAKAO BLIND RECRUITMENT > 실패율**

</br>

[연습 문제 링크](https://programmers.co.kr/learn/courses/30/lessons/42889)

</br>

:books: 내가 사용한 프로그래밍 언어 : Java  
:roller_coaster: 난이도 : Level 1

</br>

## 문제 요약

슈퍼 게임 개발자 오렐리는 동적으로 게임 시간을 늘려서 난이도를 조절하기로 했다.  
그러나 실패율을 구하는 부분에서 위기에 빠지고 말았다.  
오렐리를 위해 실패율을 구하는 코드를 완성하라.

- 실패율 = 스테이지에 도달했으나 클리어하지 못한 플레이어 수 / 스테이지에 도달한 플레이어 수

전체 스테이지 개수 N, 게임을 이용하는 사용자가 현재 멈춰있는 스테이지의 번호가 담긴 배열 stages가 매개변수로 주어질 때, 실패율이 높은 스테이지부터 내림차순으로 스테이지의 번호가 담긴 배열을 return하도록 solution 함수를 완성하라.

</br>

## 추가 사항

- 1 <= N <= 500
- 1 <= stages.length <= 200,000
- stages에는 1 이상 N + 1 이하의 자연수가 담겨 있음
  - 각 자연수는 사용자가 현재 도전 중인 스테이지의 번호를 나타냄
  - N + 1은 마지막 스테이지 N까지 클리어 한 사용자를 나타냄
  - 만약 실패율이 같은 스테이지가 있다면 작은 번호의 스테이지가 먼저 오도록 함
  - 스테이지에 도달한 유저가 없는 경우 해당 스테이지의 실패율은 0

</br>

## 다른 사람의 풀이

부끄럽게도 문제를 풀어내지 못했다.  
로직은 얼추 생각해냈으나, 2차원 배열을 Java에서는 어떻게 정렬할 수 있는지가 난감하여 한참을 해맸다.  
결국 두세 시간 동안 제자리걸음만 하고 있는 나 자신을 발견하고는 이대로는 안되겠다 싶어서 빨리 풀이를 확인하여 이해하고 짚고 넘어가기로 했다.

```java
import java.util.Collections;
import java.util.ArrayList;

class Solution {
    public int[] solution(int N, int[] stages) {
        int[] answer = new int[N];
        double[] stage = new double[N+1];      // 스테이지마다 머물러 있는 사용자수를 담을 배열

        // stage배열에 머물러있는 사용자수를 담는다 , 인덱스값이 스테이지번호
        for(int i : stages){
            if(i == N+1){
                continue;
            }
            stage[i]++;
        }

        // 실패율을 계산해 담을 list
        ArrayList<Double> fail = new ArrayList<Double>();

        //스테이지에 도달한 명수
        double num =stages.length;
        //다음 스테이지로 올라갈때 줄어드는 사용자수를 계산하기 위해 사용
        double tmp = 0;

        //실패율을 구한 후 다시 stage배열에 담고, fail 리스트에도 담아준다.
        for(int i=1; i<stage.length; i++){
            tmp = stage[i];
            // 도달한 사용자 수가 0 일때, 실패율도 0
            if(num == 0){
                stage[i]=0;
            }else{
                stage[i] = stage[i]/num;
                num = num - tmp;
            }

            fail.add(stage[i]);
      }

     //  fail 리스트를 내림차순으로 정렬해준다.
     Collections.sort(fail,Collections.reverseOrder());

     //정렬된 fail리스트 값과 stage값을 비교해서 같으면 stage의 인덱스번호(스테이지번호)를 가져옴으로써
     //실패율이 높은 순으로 answer배열에 넣어준다.
     for(int i=0; i<fail.size(); i++){
         for(int j=1; j<stage.length; j++){
             if(fail.get(i) == stage[j]){
                 answer[i] = j;
                 stage[j] = -1;
                 break;
            }
        }
    }

    return answer;
    }
}
```

주석으로 설명을 친절하게 달아주셨기에 가져와봤다.  
내가 특히 헷갈렷던 부분은 Collection.sort() 부분이다.  
Collection을 활용해 본 경험이 전무하다보니 정말 제대로 막혔었다.  
이 코드를 어느 정도 참고해서 꼭 다음에 다시 풀어봐야겠다.
