## **Programmers > 연습문제 > 핸드폰 번호 가리기**

</br>

[연습 문제 링크](https://programmers.co.kr/learn/courses/30/lessons/12948)

</br>

📚 내가 사용한 프로그래밍 언어 : Java  
🎢 난이도 : Level 1

</br>

## 문제 요약

전화번호가 문자열 phone_number로 주어졌을 때, 전화번호의 뒷 4자리를 제외한 나머지 숫자를 전부 `*` 으로 가린 문자열을 반환하라.

</br>

## 추가 사항

- 4 <= phone_number.length() <= 20

</br>

## 내 풀이 (Java)

```java
class Solution {
    public String solution(String phone_number) {
        String[] s = phone_number.split("");
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < s.length; i++) {
            if (i < s.length - 4) {
                sb.append("*");
            } else sb.append(s[i]);
        }

        return sb.toString();
    }
}
```

아직도 조금 낯선 StringBuilder를 적극 활용해서 문제를 풀어냈다.  
별도로 라이브러리를 import하지 않아도 되어서 간편하며, 사용할 메소드도 별 게 없어서 손쉬운 느낌이 들었다.

</br>

## 다른 사람의 풀이 (Java)

```java
class Solution {
  public String solution(String phone_number) {
    return phone_number.replaceAll(".(?=.{4})", "*");
  }
}
```

나도 이 문제를 처음 접했을 때, '어쩌면 정규표현식으로도 어떻게 해볼 수 있지 않을까?' 하는 생각이 들었지만, 아무래도 정규표현식 활용이 아직도 많이 안 익숙해서 금새 마음을 접었다.  
하지만 아니나 다를까, 정규표현식으로 풀어낸 분이 계셨다.  
해당 풀이 밑에 달린 댓글을 참조하여, 정규표현식이 작동하는 방식을 살펴보자면 이렇다.

1. . : 임의의 문자 1개
2. (?=.) : 뒤쪽에 임의의 문자 한개를 제외하고 선택
3. {4} : 숫자 만큼의 자릿수
4. .(?=.{4}) : 뒤쪽에서 임의의 문자 4개를 제외한 임의의 문자 한개 선택
