## **Programmers > 2018 KAKAO BLIND RECRUITMENT > [1차] 다트 게임**

</br>

[연습 문제 링크](https://programmers.co.kr/learn/courses/30/lessons/17682)

</br>

:books: 내가 사용한 프로그래밍 언어 : Java, JavaScript  
:roller_coaster: 난이도 : Level 1

</br>

## 문제 요약

카카오톡 게임별의 하반기 신규 서비스로 다트 게임을 출시하기로 했다.  
다트 게임의 점수 계산 로직은 다음과 같다.

1. 다트 게임은 총 3번의 기회로 구성된다.
2. 각 기회마다 얻을 수 있는 점수는 0점에서 10점까지이다.
3. 점수와 함께 Single(`S`), Double(`D`), Triple(`T`) 영역이 존재하고 각 영역 당첨 시 점수에서 1제곱, 2제곱, 3제곱으로 계산된다.
4. 옵션으로 스타상(`*`), 아차상(`#`)이 존재하며 스타상(`*`) 당첨 시 해당 점수와 바로 전에 얻은 점수를 각 2배로 만든다.  
   아차상(`#`) 당첨 시 해당 점수는 마이너스된다.
5. 스타상(`*`)은 첫 번째 기회에서도 나올 수 있다.  
   이 경우 첫 번째 스타상(`*`)의 점수만 2배가 된다.
6. 스타상(`*`)의 효과는 다른 스타상(`*`)의 효과와 중첩될 수 있다.  
   이 경우 중첩된 스타상(`*`)의 점수는 4배가 된다.
7. 스타상(`*`)의 효과는 아차상(`#`)의 효과와 중첩될 수 있다.  
   이 경우 중첩된 아차상(`#`)의 점수는 -2배가 된다.
8. Single(`S`), Double(`D`), Triple(`T`)은 점수마다 하나씩 존재한다.
9. 스타상(`*`), 아차상(`#`)은 점수마다 둘 중 하나만 존재할 수 있으며, 존재하지 않을 수도 있다.

0~10의 정수와 문자 S, D, T, \*, #으로 구성된 문자열이 입력될 시 총 점수를 반환하는 함수를 작성하라.

</br>

## 내풀이 (JavaScript)

```javascript
function solution(dartResult) {
  var answer = 0;
  let prevNum = 0;
  let num = 0;

  for (let i = 0; i < dartResult.length; i++) {
    if (!isNaN(dartResult[i])) {
      prevNum = num;
      if (dartResult[i] === "1") {
        if (dartResult[i + 1] === "0") num = 10;
        else num = 1;
      } else if (dartResult[i] === "0") {
        if (dartResult[i - 1] !== "1") num = 0;
      } else num = Number(dartResult[i]);
    }

    if (dartResult[i] === "S") {
      answer += num;
    }
    if (dartResult[i] === "D") {
      num = Math.pow(num, 2);
      answer += num;
    }
    if (dartResult[i] === "T") {
      num = Math.pow(num, 3);
      answer += num;
    }

    if (dartResult[i] === "*") {
      answer += prevNum + num;
      prevNum *= 2;
      num *= 2;
    }
    if (dartResult[i] === "#") {
      answer -= num * 2;
      num *= -1;
    }
  }

  return answer;
}
```

그동안 잘 활용해보지 않았던 isNaN을 활용해서 문제를 풀어보았다.  
그리고 전체적인 풀이는 변수 2개를 선언해서 이전 단계에서 추가한 점수를 간단하게 기억해두는 용도로 활용했다.  
살짝 헷갈릴만한 로직은 0과 10에 대한 처리이다.  
for문을 돌면서 !isNaN을 통해 숫자로된 문자 값을 찾아내기 때문에 10을 만났을 때 다소 난감하다.  
그래서 겹겹이 조건문을 활용해서 이에 대처했다.  
하지만 아래에 Java 풀이를 확인해보면 더 나은 방법이 있음을 확인할 수 있을 것이다.

</br>

## 내 풀이 (Java)

```java
class Solution {
    public int solution(String dartResult) {
        int answer = 0;
        int prevNum = 0;
        int num = 0;

        for (int i = 0; i < dartResult.length(); i++) {
            char c = dartResult.charAt(i);
            if (Character.isDigit(c)) {
                prevNum = num;
                num = c - '0';
                if (num == 1) {
                    if (dartResult.charAt(i + 1) == '0') {
                        num = 10;
                        i++;
                    }
                    else num = 1;
                }
            }

            if (c == 'S') {
                answer += num;
            }
            if (c == 'D') {
                num *= num;
                answer += num;
            }
            if (c == 'T') {
                num *= num * num;
                answer += num;
            }

            if (c == '*') {
                answer += prevNum + num;
                prevNum *= 2;
                num *= 2;
            }
            if (c == '#') {
                answer -= (num * 2);
                num *= -1;
            }
        }

        return answer;
    }
}
```

전체적인 로직의 흐름은 똑같게 작성을 했었다.  
하지만 어째서인지 32개의 테스트 케이스 중 5번과 8번만 계속해서 런타임 에러로 실패하는 모습을 확인할 수 있었다.  
삽질을 좀 하다가 '다른 사람의 풀이' 탭을 확인해봤는데, 거기에서 문자로 된 숫자 10을 만났을 때, i++을 활용해서 건너뛰어 주는 로직을 발견할 수 있었다.  
이를 그대로 적용해보니 무사히 모든 테스트 케이스를 통과할 수 있었다.  
정말 단순한 로직이지만 보다 효율적인 방법이었다.  
또한 나는 Character 타입에 isDigit() 같은 메소드가 있다는 사실을 몰랐었다.  
아직도 효율적으로 로직을 짜는 방법이나 적절한 메소드를 활용하는 방법을 잘 모르는 느낌이다.  
오늘 배운 방법들을 꼭 유념해두자.

</br>

## 다른 사람의 풀이 (JavaScript)

```javascript
function solution(dartResult) {
  const bonus = { S: 1, D: 2, T: 3 },
    options = { "*": 2, "#": -1, undefined: 1 };

  let darts = dartResult.match(/\d.?\D/g);

  for (let i = 0; i < darts.length; i++) {
    let split = darts[i].match(/(^\d{1,})(S|D|T)(\*|#)?/),
      score = Math.pow(split[1], bonus[split[2]]) * options[split[3]];

    if (split[3] === "*" && darts[i - 1]) darts[i - 1] *= options["*"];

    darts[i] = score;
  }

  return darts.reduce((a, b) => a + b);
}
```

정규표현식을 활용한 방법이다.  
아직도 정규표현식은 쉽사리 이해가 되질 않는다.  
확실히 정규표현식을 좀 더 공부해야 할 필요성을 느낀다.  
이렇게 옮겨적는 것으로 그칠 것이 아니라, 직접 활용해보고 연습해보는 과정을 거쳐야만 하겠다.

</br>

사실 테스트 통과 속도는 내 코드가 약 2배 정도 빨랐다.  
(내 코드 : 약 0.15ms / 정규식을 활용한 코드 : 약 0.3ms)  
사실 둘 다 빨라서 뭐가 되었든 상관 없긴 하다.  
그래도 차이가 생기는 이유를 유추해보자면 아마도 정규표현식으로 문자열을 가려내는 과정에서 쪼끔 더 시간을 잡아먹지 않았나 싶다.  
테스트 통과 시간이야 어쨌든 정규표현식은 꼭 익혀두어야겠다는 생각이 든다.  
그래야 앞으로 문자열 관련 문제들을 풀어나갈 때 유용하게 활용할 수 있을 것 같다.
