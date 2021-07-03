## **Programmers > 2021 KAKAO BLIND RECRUITMENT > 신규 아이디 추천**

</br>

[연습 문제 링크](https://programmers.co.kr/learn/courses/30/lessons/72410)

</br>

---

</br>

:books: 내가 사용한 프로그래밍 언어 : Java, JavaScript

</br>

## 문제 요약

카카오에 새로 가입하는 유저들이 카카오 아이디 규칙에 맞지 않는 아이디를 입력했을 때, 입력된 아이디와 유사하면서 규칙에 맞는 아이디를 추천해주는 프로그램을 개발한다.  
다음은 카카오 아이디의 규칙이다.

- 아이디의 길이는 3자 이상 15자 이하
- 아이디는 알파벳 소문자, 숫자, 빼기(-), 밑줄(\_), 마침표(.)만 사용 가능
- 마침표(.)는 처음과 끝에 사용 불가능, 연속 사용도 불가능

7단계의 순차적인 처리 과정을 통해 신규 유저의 아이디를 검사하고 규칙에 맞지 않을 경우 새로운 아이디를 추천한다.  
신규 유저가 입력한 아이디가 new_id라고 한다면,

1. new_id의 모든 대문자를 소문자로 치환
2. new_id에서 알파벳 소문자, 숫자, 빼기(-), 밑줄(\*), 마침표(.)를 제외한 모든 문자 제거
3. new_id에서 마침표(.)가 2번 이상 연속된 부분을 하나의 마침표(.)로 치환
4. new_id에서 마침표(.)가 처음이나 끝에 위치한다면 제거
5. new_id가 빈 문자열이라면, new_id에 "a"를 대입
6. new_id의 길이가 16자 이상이면 첫 15개의 문자를 제외한 나머지 문자들 제거
7. new_id의 길이가 2자 이하라면 마지막 문자를 길이가 3이 될 때까지 반복해서 끝에 붙임

</br>

## 추가 사항

- new_id는 길이 1 이상 1,000 이하인 문자열
- new_id는 알파벳 대문자 및 소문자, 숫자, 특수문자로 구성됨
- new_id에 나타날 수 있는 특수문자는 <span class="evidence">-\*.~!@#$%^&\*()=+[{]}:?,<>/</span> 로 한정됨

</br>

## 풀이

친절하게도 문자열을 어떻게 치환해나가면 될지에 대해 7단계에 걸쳐서 알려주고 있다.  
그래서 나는 replaceAll() 메소드를 사용해서 각 단계를 하나씩 처리해주었다.  
첫 풀이는 **Java** 언어를 사용했다.

1단계. 대문자를 소문자로

```java
String answer = new_id.toLowerCase();
```

2단계. 조건 외 다른 문자 제거

```java
answer = answer.replaceAll("[^-_.a-z0-9]", "");
```

3단계. 마침표가 2번 이상 연속되면 하나의 마침표로 치환

```java
answer = answer.replaceAll("[.]{2,}", ".");
```

4단계. 마침표가 처음이나 끝에 있으면 제거

```java
answer = answer.replaceAll("^[.]|[.]$", "");
```

5단계. 빈 문자열이라면 "a" 반환

```java
if (answer.equals("")) {
    answer += "a";
}
```

6단계. 길이가 16자 이상이면 15개를 제외한 나머지 제거

```java
if (answer.length() >= 16) {
    answer = answer.substring(0, 15);
    answer = answer.replaceAll("^[.]|[.]$", "");
}
```

7단계. 길이가 2자 이하면 3이 될 때 까지 마지막 문자 반복

```java
if (answer.length() <= 2) {
    while (answer.length() < 3) {
        answer += answer.charAt(answer.length()-1);
    }
}
```

</br>

## 해답

### **Java**

```java
class Solution {
    public String solution(String new_id) {
        String id = new_id.toLowerCase();
        id = id.replaceAll("[^-_.a-z0-9]", "");
        id = id.replaceAll("[.]{2,}", ".");
        id = id.replaceAll("^[.]|[.]$", "");

        if(id.equals(""))
            id += "a";

        if(id.length() >= 16){
            id = id.substring(0, 15);
            id = id.replaceAll("^[.]|[.]$", "");
        }
        if(id.length() <= 2)
            while(id.length() < 3)
                id += id.charAt(id.length() - 1);

        return id;
    }
}
```

### **JavaScript**

```javascript
function solution(new_id) {
  new_id = new_id
    .toLowerCase()
    .replace(/[^\w\.\-]/g, "")
    .replace(/[\.]{2,}/g, ".")
    .replace(/^\./, "")
    .replace(/\.$/, "");
  if (!new_id) {
    new_id = "a";
  }
  if (new_id.length >= 16) {
    new_id = new_id.slice(0, 15).replace(/\.$/, "");
  }
  if (new_id.length <= 2) {
    new_id = new_id.padEnd(3, new_id[new_id.length - 1]);
  }
  return new_id;
}
```

</br>

## 소감

프로그래머스 사이트의 코딩 테스트 연습 레벨 1 중에서도 내 수준에 맞는 간단한 문제였다.  
하지만 나는 사실 정규 표현식도 제대로 정리가 안 되어 있었기 때문에 꽤 애를 먹었다. :sweat_smile:  
그래도 이 문제는 내가 코딩 테스트 연습 사이트에서 처음으로 제대로 푼 문제가 되어주었고, 나도 아주 조금은 문제 풀이에 자신감을 가질 수 있게 해주었다.  
천리길도 한걸음부터 :exclamation:  
지금은 아직 코딩 테스트 연습 문제들을 봐도 어떻게 풀어야 할지 감도 안오고 답답하지만 답지들을 보고서라도 연습을 해가면서 내가 풀 수 있는 문제들의 영역을 넓혀가자.  
그리고 정규 표현식에 관련해서는 따로 공부를 해서 꼭 TIL에 정리해야겠다.
