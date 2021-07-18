bㅠ## **Programmers > 2021 카카오 채용연계형 인턴십 > 숫자 문자열과 영단어**

</br>

[연습 문제 링크](https://programmers.co.kr/learn/courses/30/lessons/81301)

</br>

:books: 내가 사용한 프로그래밍 언어 : Java
:roller_coaster: 난이도 : Level 1

</br>

## 문제 요약

네오와 프로도가 숫자놀이를 하고 있다.  
네오가 프로도에게 숫자를 건넬 때 일부 자릿수를 영단어로 바꾼 카드를 건네주면 프로도는 원래 숫자를 찾는 게임이다.

</br>

다음은 영단어에서 숫자로 바꾸는 예시이다.

- "one4seveneight" → 1478
- "23four5six7" → 234567
- "1zerotwozero3" → 10203

이처럼 숫자의 일부 자릿수가 영단어로 바뀌어졌거나, 혹은 바뀌지 않고 그대로인 문자열 s가 매개변수로 주어진다.  
s가 의미하는 원래 숫자를 return하라.

</br>

## 추가 사항

- 1 <= s <= 50
- s가 "zero" 또는 "0"으로 시작하는 경우는 없음
- return 값이 1 이상 2,000,000,000 이하의 정수가 되는 문자열만 주어짐
- 정확성 테스트 : 10초

</br>

## 내 풀이 (오답)

```java
class Solution {
    public int solution(String s) {
        int answer = 0;
        String letter = "";
        for (int i = 0; i < s.length(); i++) {
            if (48 <= s.charAt(i) && s.charAt(i) <= 57) {
                letter += s.charAt(i);
            } else if (s.charAt(i) == 122) {
                if (i + 3 < s.length() && s.charAt(i + 3) == 111) {
                    letter += "0";
                }
            } else if (s.charAt(i) == 111) {
                if (i + 2 < s.length() && s.charAt(i + 2) == 101) {
                    letter += "1";
                }
            } else if (s.charAt(i) == 116) {
                if (i + 4 < s.length() && s.charAt(i + 4) == 101) {
                    letter += "3";
                } else if (i + 2 < s.length() && s.charAt(i + 2) == 111) {
                    letter += "2";
                }
            } else if (s.charAt(i) == 102) {
                if (i + 3 < s.length() && s.charAt(i + 3) == 114) {
                    letter += "4";
                } else if (s.charAt(i + 3) == 101) {
                    letter += "5";
                }
            } else if (s.charAt(i) == 115) {
                if (i + 4 < s.length() && s.charAt(i + 4) == 110) {
                    letter += "7";
                } else if (i + 2 < s.length() && s.charAt(i + 2) == 120) {
                    letter += "6";
                }
            } else if (s.charAt(i) == 101) {
                if (i + 4 < s.length() && s.charAt(i + 4) == 116) {
                    letter += "8";
                }
            } else if (s.charAt(i) == 110) {
                if (i + 3 < s.length() && s.charAt(i + 3) == 101) {
                    letter += "9";
                }
            }
        }
        answer = Integer.parseInt(letter);
        return answer;
    }
}
```

이 문제를 풀기 몇 시간 전에 풀었던 [백준 곱셈 문제](https://github.com/nmin11/Programming_Exercise/blob/main/Mathematics/Baekjoon%20-%20%EA%B3%B1%EC%85%88.md)를 풀면서 charAt 메소드에 꽂혀 있었던지 charAt 메소드를 굉장히 무리해서 사용했다.  
"코드 실행" 탭의 4가지 테스트 케이스는 다 통과할 수 있었지만, "제출하기" 탭의 10가지 테스트 케이스 중 1개는 실패했고, 1개는 런타임 10초를 초과해버렸다.  
어떻게 수정해도 이 방법으로는 도저히 해답을 찾아낼 수 없겠다는 것을 느끼고 결국 구글링을 통해 해결을 보았다.

</br>

## 다른 사람의 풀이

```java
class Solution {
    public int solution(String s) {
        String[] strArr = {"zero", "one", "two", "three", "four", "five", "six", "seven", "eight", "nine"};
        for(int i = 0; i < strArr.length; i++) {
            s = s.replaceAll(strArr[i], Integer.toString(i));
        }
        return Integer.parseInt(s);
    }
}
```

너무 안타까웠다.  
이미 다 알고 있었던 메소드들이고, 충분히 내 힘으로도 풀 수 있었던 문제다.  
아직도 문제를 넓게 보는 시각이 너무나도 부족하다는 것을 느낀다.
