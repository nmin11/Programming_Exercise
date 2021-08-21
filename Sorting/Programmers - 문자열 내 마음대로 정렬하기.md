## **Programmers > 연습문제 > 문자열 내 마음대로 정렬하기**

</br>

[연습 문제 링크](https://programmers.co.kr/learn/courses/30/lessons/12915)

</br>

📚 내가 사용한 프로그래밍 언어 : Java, JavaScript  
🎢 난이도 : Level 1

</br>

## 문제 요약

문자열로 구성된 배열 strings와 정수 n이 주어졌을 때, 각 문자열의 인덱스 n번째 문자를 기준으로 오름차순으로 정렬하라.

</br>

## 추가 사항

- 1 <= strings.length <= 50
- strings[i]는 소문자 알파벳으로 이루어져 있음
- 1 <= strings[i].length <= 100
- 모든 strings[i]는 n보다 큼
- 인덱스 n의 문자가 같은 문자열이 여럿 일 경우, 사전순으로 앞선 문자열이 앞쪽에 위치

</br>

## 내 풀이 (오답) (JavaScript)

```javascript
function solution(strings, n) {
  return strings.sort((a, b) => a[n] - b[n]);
}
```

사실, 아직도 이게 왜 제대로 작동하지 않는지 그 원인에 대해서 이해하지는 못했다.  
그래도 이게 올바른 방법이 아니라는 것을 깨달았지만, 뾰족한 수가 떠오르지 않아서 다른 사람의 풀이를 참조하고 넘어가기로 했다.

</br>

## 다른 사람의 풀이 (JavaScript)

```javascript
function solution(strings, n) {
  let answer = strings.sort((a, b) => {
    if (a[n] > b[n]) return 1;
    if (a[n] < b[n]) return -1;
    else {
      if (a > b) return 1;
      if (a < b) return -1;
      else return 0;
    }
  });

  return answer;
}
```

JavaScript의 sort 메소드를 보다 정석적으로 활용했음을 알 수 있었다.  
상황에 맞게 sort 메소드를 올바르게 활용하는 방법을 확실하게 익혀둬야만 하겠다.

</br>

## 다른 사람의 풀이 (Java)

```java
import java.util.*;

class Solution {
  public String[] solution(String[] strings, int n) {
      Arrays.sort(strings, new Comparator<String>(){
          @Override
          public int compare(String s1, String s2){
              if(s1.charAt(n) > s2.charAt(n)) return 1;
              else if(s1.charAt(n) == s2.charAt(n)) return s1.compareTo(s2);
              else if(s1.charAt(n) < s2.charAt(n)) return -1;
              else return 0;
          }
      });
      return strings;
  }
}
```

솔직히, 이 문서를 작성하게 된 계기는 여기에 있다.  
사실 간단한 로직을 가진 문제라 가볍게 확인하고 넘어갈 수도 있었지만 이 Java 풀이 방법이 생소했고, 또한 상당히 유용한 풀이 방법이라는 사실을 깨달았기 때문에 이렇게 옮겨적어 보게 되었다.  
Comparator의 활용에 대해서 추후에 TIL에 정리해봐야만 하겠다.
