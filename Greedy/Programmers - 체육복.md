## **Programmers > Greedy > 체육복**

</br>

[연습 문제 링크](https://programmers.co.kr/learn/courses/30/lessons/42862)

</br>

:books: 내가 사용한 프로그래밍 언어 : Java, JavaScript  
:roller_coaster: 난이도 : Level 1

</br>

## 문제 요약

점심시간에 도둑이 들어, 일부 학생들이 체육복을 도난당했다.  
다행히 여벌 체육복이 있는 학생들이 이들에게 체육복을 빌려주려 한다.  
하지만 학생들은 바로 앞번호의 학생이나 바로 뒷번호의 학생에게만 체육복을 빌려줄 수 있다.  
체육복을 적절히 빌려서 최대한 많은 학생이 체육 수업을 들어야 한다.

</br>

## 추가 사항

- 전체 학생의 수는 2명 이상 30명 이하
- 체육복을 도난당한 학생의 수는 1명 이상 n명 이하, 중복되는 번호는 없음
- 여벌 체육복을 가져온 학생의 수는 1명 이상 n명 이하, 중복되는 번호는 없음
- 여벌 체육복이 있는 학생만 다른 학생에게 체육복을 빌려줄 수 있음
- 여벌 체육복을 가져온 학생이 체육복을 도난당했을 수 있음, 이 때 도난 당한 체육복은 하나, 여벌 체육복도 하나라고 가정하며, 남은 체육복이 하나이기에 다른 학생에게는 체육복을 빌려줄 수 없음

</br>

## 첫 풀이 (오답)

**Java** 언어를 사용해서 나름대로 머리를 굴려가며 다음과 같은 코드를 작성했다.

```java
class Solution {
    public int solution(int n, int[] lost, int[] reserve) {
        int answer = n - lost.length;
        for (int i = 0; i < lost.length; i++) {
            for (int j = 0; j < reserve.length; j++) {
                if (lost[i] != -1 && reserve[j] != -1) {
                    if (lost[i] - 1 == reserve[j] || lost[i] + 1 == reserve[j]) {
                        reserve[j] = -1;
                        lost[i] = -1;
                        answer++;
                    }
                }
            }
        }
        return answer;
    }
}
```

간단하게 설명하자면, 체육복을 도난당한 사람의 번호의 +1 혹은 -1 한 값이 여분을 갖고 있는 사람의 번호와 일치하면 둘 다 -1이라는 임의의 번호로 예외를 시키면서 체육복을 가지고 있는 사람의 총원을 ++ 해주는 것이다.  
위 코드를 가지고 제출 전의 테스트 케이스를 돌려본 결과, 단 2개의 테스트 케이스가 있었고, 모두 통과했다.  
하지만 제출을 눌러보니 총 12개의 테스트를 돌렸으며, 그 중 5개가 틀려서 최종 제출에 실패했다.  
무엇이 문제였던 것일까?  
</br>
해당 문제 안의 질문하기 버튼을 눌러서 혹시라도 나와 유사한 문제를 겪고 있는 사람이 있는지 확인해보았다.  
확인해보니, 질문을 올린 사람들이 제출 테스트에서 실패한 테스트 번호들이 내가 실패한 테스트 번호들과 상당히 유사하다는 점을 알 수 있었다.  
그래서 해당 질문 케이스들을 눌러보면서 무엇이 문제였는지 확인해보았고, 간단하게 문제의 원인을 파악할 수 있었다.  
</br>
문제의 원인은 바로, 여분의 체육복을 가지고 있으면서 체육복을 도난당했을 가능성을 생각하지 못했다는 것이었다.  
이 경우에는 lost 배열에도 번호가 들어가고 reserve 배열에도 번호가 들어가게 되는 것이다.  
사실 간단하게 말해서, 추가 사항을 제대로 읽어보지를 않았던 것이다. :sweat_smile:

</br>

## 수정한 풀이

```java
class Solution {
    public int solution(int n, int[] lost, int[] reserve) {
        for (int i = 0; i < reserve.length; i++) {
            for (int j = 0; j < lost.length; j++) {
                if (lost[j] == reserve[i]) {
                    lost[j] = -1;
                    reserve[i] = -1;
                }
            }
        }
        int answer = n;
        for (int i = 0; i < lost.length; i++) {
            if (lost[i] != -1) {
                answer--;
            }
            for (int j = 0; j < reserve.length; j++) {
                if (lost[i] != -1 && reserve[j] != -1) {
                    if (lost[i] - 1 == reserve[j] || lost[i] + 1 == reserve[j]) {
                        reserve[j] = -1;
                        lost[i] = -1;
                        answer++;
                    }
                }

            }
        }
        return answer;
    }
}
```

기존 코드의 위쪽에 lost와 reserve의 번호가 겹치는 부분에 대해서 똑같이 -1이라는 임의의 번호를 주었다.  
그렇게만 하면 역시 테스트가 실패한다.  
왜냐하면 기존의 let answer = n - lost.length; 라는 코드는 위에서 처리한 겹치는 인원들도 다 포함 되기 때문이다.  
따라서 answer 변수에 총원을 그냥 담아두고 lost[i] != -1 인 경우에만 총원에서 빼주는 식으로 코드를 변경했다.  
그렇게 해서 제출 테스트를 모두 통과할 수 있었지만 뭔가 for문과 if문의 남발한 것 같다는 생각이 든다.

</br>

## 다른 사람의 풀이

```java
class Solution {
    public int solution(int n, int[] lost, int[] reserve) {
        int[] people = new int[n];
        int answer = n;

        for (int l : lost)
            people[l-1]--;
        for (int r : reserve)
            people[r-1]++;

        for (int i = 0; i < people.length; i++) {
            if(people[i] == -1) {
                if(i - 1 >= 0 && people[i-1] == 1) {
                    people[i]++;
                    people[i-1]--;
                }else if(i + 1 < people.length && people[i+1] == 1) {
                    people[i]++;
                    people[i+1]--;
                }else
                    answer--;
            }
        }
        return answer;
    }
}
```

솔직히 한 눈에 딱 보고 이해가 되지는 않지만 내 나름대로 유추해보자면 이렇다.  
일단 총원 숫자 만큼 int값들을 담을 수 있는 people이라는 새 배열 변수를 선언한다.  
내 생각이 맞다면 총원 수 만큼의 0들이 이 배열에 담겨 있을 것이다.  
그 다음, 새 배열 안에서 체육복이 필요한 사람은 -1이라는 값을, 여분이 있는 사람은 1이라는 값을 할당해준다.  
이렇게 얻게 된 people 변수를 for문으로 돌리면서, people이 체육복이 없는 사람인 경우에만 연산을 진행한다.  
안쪽 첫 if문에서는 체육복이 없는 사람의 이전 번호가 여분이 있을 경우 두 사람 다 0이라는 값을 넣어준다.  
그 다음 else if문에서는 체육복이 없는 사람의 다음 번호가 여분이 있을 경우 두 사람 다 0이라는 값을 넣어준다.  
이런 작업들을 수행하지 못한다면 총원에서 -1 씩 해준 뒤, 마지막에 그 값을 반환하는 것이다.

</br>

## JavaScript 풀이

위의 '다른 사람의 풀이'를 참조하여 JavaScript로도 풀어보았다.

```javascript
function solution(n, lost, reserve) {
  let answer = n;
  let people = Array(n).fill(0);

  for (let l of lost) people[l - 1]--;
  for (let r of reserve) people[r - 1]++;

  for (let i = 0; i < people.length; i++) {
    if (people[i] === -1) {
      if (i - 1 >= 0 && people[i - 1] === 1) {
        people[i]++;
        people[i - 1]--;
      } else if (i + 1 < people.length && people[i + 1] === 1) {
        people[i]++;
        people[i + 1]--;
      } else answer--;
    }
  }

  return answer;
}
```
