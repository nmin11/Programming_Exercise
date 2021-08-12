## **Programmers > 위클리 챌린지 2주차 > 상호 평가**

</br>

[연습 문제 링크](https://programmers.co.kr/learn/courses/30/lessons/83201)

</br>

:books: 내가 사용한 프로그래밍 언어 : Java  
:roller_coaster: 난이도 : Level 1

</br>

## 문제 요약

정수형 2차원 배열이 주어진다.  
배열 속 값들은 i가 평가해준 j의 성적들을 뜻한다.  
만약 자기가 평가한 점수가 **유일한 최고점**이거나, **유일한 최저점**이라면, 해당 점수는 제외하고 평균 점수를 구한다.  
평균 점수를 토대로 아래 기준에 따라 학점을 부여한다.

|        평균         | 학점 |
| :-----------------: | :--: |
|      90점 이상      |  A   |
| 80점 이상 90점 미만 |  B   |
| 70점 이상 80점 미만 |  C   |
| 50점 이상 70점 미만 |  D   |
|      50점 미만      |  F   |

모든 학생들의 학점을 하나의 문자열로 합쳐서 리턴하라.

</br>

## 추가 사항

- 2 <= scores.length <= 10
- 주어진 배열은 정사각형의 2차원 배열
- 0 <= scores[i][j] <= 100

</br>

## 내 풀이 (Java)

```java
public String solution(int[][] scores) {
    String answer = "";

    for (int i = 0; i < scores.length; i++) {
        int sum = 0;
        int mine = scores[i][i];
        int max = scores[i][i];
        int min = scores[i][i];

        for (int j = 0; j < scores.length; j++) {
            if (i != j && scores[j][i] >= mine) {
                max = -1;
            }

            if (i != j && scores[j][i] <= mine) {
                min = -1;
            }

            sum += scores[j][i];
        }
        int total = scores.length;
        if (max != -1 || min != -1) {
            sum -= mine;
            total--;
        };
        int avg = sum / total;

        switch (avg / 10) {
            case 9 :
                answer += "A";
                break;
            case 8 :
                answer += "B";
                break;
            case 7 :
                answer += "C";
                break;
            case 6 :
                answer += "D";
                break;
            case 5 :
                answer += "D";
                break;
            default :
                answer += "F";
                break;
        }
    }

    return answer;
}
```

단순하게 접근했다.  
이중 반복문을 통해 모든 요소들을 확인하면서 동시에 최대값과 최소값을 판별하는 로직을 짰다.  
mine 값이 유일한 최대값이 되거나 유일한 최소값이 될 수 있는지만 판별해서, 만약 그런 값이 될 수 없다면 -1이라는 식별 전용 숫자를 넣어줬다.  
이후 max나 min 둘 중 하나라도 -1이 아닌 어떤 값을 가지고 있다면 총합에서 자기 점수를 빼고, 총 인원에서도 1을 빼서 평균을 구하는 로직이다.

</br>

## 다른 사람의 풀이 (Java)

```java
public String solution(int[][] scores) {
    StringBuilder builder = new StringBuilder();
    for(int i=0; i<scores.length; i++) {
        int max = 0;
        int min = 101;
        int sum = 0;
        int divide = scores.length;
        for(int j=0; j<scores.length; j++) {
            int score = scores[j][i];
            if(i != j) {
                if(score < min) {
                    min = score;
                }
                if(score > max) {
                    max = score;
                }
            }
            sum += score;
        }
        if(scores[i][i] < min || scores[i][i] > max) {
            sum -= scores[i][i];
            divide--;
        }
        double score = (double) sum / divide;
        builder.append(score >= 90 ? "A" : score >= 80 ? "B" : score >= 70 ? "C" : score >= 50 ? "D" : "F" );
    }
    return builder.toString();
}
```

전체적인 접근 방식은 나와 비슷한 것 같은데, 테스트 통과 속도가 상당히 빠른 코드였다.  
(내 코드는 테스트 통과 시간이 2ms 정도가 나왔는데 이 코드는 거의 0.03ms가 나온다)  
똑같은 이중 반복문을 사용했음에도 테스트 속도가 이렇게 다르다는 사실에 무척 놀랐다.  
StringBuilder를 활용하는 방법을 익혀둬야만 하겠다.

</br>

## 다른 사람의 풀이 (JavaScript)

```javascript
let solution = (scores) =>
  scores[0]
    .map((_, c) => scores.map((r) => r[c]))
    .map((s, i) => [...s.splice(i, 1), s])
    .map(([m, s]) =>
      Math.min(...s) <= m && m <= Math.max(...s) ? [m, ...s] : s
    )
    .map(
      (s) =>
        "FDDCBAA"[
          Math.max(parseInt(s.reduce((a, c) => a + c) / s.length / 10) - 4, 0)
        ]
    )
    .join("");
```

어짜피 내가 직접 JavaScript로 다시 풀면 똑같은 로직을 그대로 구현할 것이 뻔하기 때문에 JavaScript에서 다른 사람들은 어떻게 풀었는지 바로 살펴보았다.  
최상단에 이러한 코드가 있었는데 참 이해가 되질 않는다. 😂  
map 같은 메소드는 분명 어떤 메소드인지 인지를 하고 있는데도 머릿속에 쉽게 들어오지 않는다.  
시간을 두고 계속 보면서 이해해보는 시간을 따로 가져야만 하겠다.  
코드만 짧은게 아니라 테스트 통과 시간도 0.2ms로 꽤나 준수한 속도를 가진 로직임을 확인할 수 있었다.
