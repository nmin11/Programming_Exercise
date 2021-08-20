## **Programmers > 2018 KAKAO BLIND RECRUITMENT > [1차] 비밀지도**

</br>

[연습 문제 링크](https://programmers.co.kr/learn/courses/30/lessons/17681)

</br>

:books: 내가 사용한 프로그래밍 언어 : JavaScript  
:roller_coaster: 난이도 : Level 1

</br>

## 문제 요약

2차원 배열로 이루어진 지도가 2장이 있다.  
지도는 숫자로 암호화되어 있어서 해독해야 하며, 그 방법은 다음과 같다.

1. 지도는 한 변의 길이가 n인 정사각형 배열 형태이며, 각 칸은 " "(공백) 또는 "#"(벽) 두 종류로 이루어져 있다.
2. 전체 지도는 두 장의 지도를 겹쳐서 얻을 수 있다.  
   arr1과 arr2 둘 중 하나라도 벽인 부분은 전체 지도에서 벽이다.  
   arr1과 arr2 둘 다 공백인 부분은 지도에서도 공백이다.
3. arr1과 arr2는 각각 정수 배열로 암호화되어 있다.
4. 암호화된 베열은 지도의 각 가로줄에서 벽 부분을 1, 공백 부분을 0으로 부호화했을 때 얻어지는 이진수에 해당하는 값의 배열이다.

비밀지도를 해독하여 "#" 또는 " "으로 구성된 문자열 배열로 리턴하라.

</br>

## 예시

![비밀지도](https://user-images.githubusercontent.com/75058239/130169480-960cc0bd-4cb7-4998-862a-6e83561767cb.png)

</br>

## 추가 사항

- 1 <= n <= 16
- arr1.length == arr2.length == n
- 정수 배열의 각 원소 x를 이진수로 변환했을 때의 길이는 n 이하  
  0 <= x <= 2ⁿ-1

</br>

## 내 풀이 (JavaScript)

```javascript
function solution(n, arr1, arr2) {
  var answer = [];

  for (let i = 0; i < n; i++) {
    let str = arr1[i].toString(2);
    while (str.length < n) {
      str = "0" + str;
    }
    answer.push(str);

    str = arr2[i].toString(2);
    while (str.length < n) {
      str = "0" + str;
    }

    let newStr = "";
    for (let j = 0; j < n; j++) {
      let el = answer[i];
      if (el[j] === "1" || str[j] === "1") {
        newStr += "#";
      } else {
        newStr += " ";
      }
    }
    answer[i] = newStr;
  }

  return answer;
}
```

원래는 str.concat() 메소드를 활용해서 문제를 풀어보려고 했으나, 에러가 자꾸 발생해서 그냥 직접 더해주는 방식으로 고쳤다.  
확인해보니, concat의 경우 초기값이 null이면 안된다는 이슈가 있었다.  
꼭 확인해두고 나중에 같은 실수를 반복하지 않도록 하자.

</br>

## 다른 사람의 풀이 (JavaScript)

```javascript
function solution(n, arr1, arr2) {
  return arr1.map((v, i) =>
    addZero(n, (v | arr2[i]).toString(2)).replace(/1|0/g, (a) =>
      +a ? "#" : " "
    )
  );
}

const addZero = (n, s) => {
  return "0".repeat(n - s.length) + s;
};
```

나도 문제를 풀면서 '정규표현식을 활용해볼 수도 있겠다'는 생각은 들었지만 아직도 정규표현식의 활용이 너무 안 익숙해서 접근해보지 못했다.  
이런 식으로라도 기록해놓으며 꼭 익숙해지도록 노력하자.

</br>

## 다른 사람의 풀이 (Java)

```java
class Solution {
    public String makeSharp(int n, int m) {
        if(n == 0) {
            if( m > 0) {
                String str = "";
                for(int i = 0; i < m; i++) {
                    str += " ";
                }
                return str;
            }
            else return "";
        }
        else {
            return n % 2 == 0 ? makeSharp(n/2, m-1) + " " : makeSharp(n/2, m-1) + "#";
        }
    }
    public String[] solution(int n, int [] arr1, int [] arr2) {
        String [] answer = new String[n];
        int [] secretMap = new int[n];
        for(int i = 0; i < n; i++) {
            secretMap[i] = arr1[i] | arr2[i];
            answer[i] = makeSharp(secretMap[i], n);
        }
        return answer;
    }
}
```

사실 Java 풀이들을 쭉 훑어봤는데 이해가 안되고 난해한 풀이들이 많았다.  
아직 메소드들에 익숙하지 않아서 그렇다.  
Java 기본서를 공부하든 어떻게 하든 Java 메소드를 꼭 정리해놓을 필요가 있다고 느낀다.

</br>

위 풀이는 재귀함수를 활용해서 문제를 풀어냈다.

```java
// 10진법 -> 3진법(역순)
while(true) {
    if(n < 3) { temp.add(n); break; }
    temp.add(n % 3);
    n = n / 3;
}
```

이전에 '3진법 뒤집기' 라는 문제를 풀면서 이런 연산 과정을 확인할 수 있었는데, 같은 연산 방법을 활용한 것 같다.  
눈에 익지도 않고, Java에서 2진법, 3진법 등을 다루는 과정이 JavaScript에 비해서 너무 난해하게 느껴진다.  
계속 눈에 익히고 또 직접 활용도 해보면서 익숙해지는 수 밖에 없다.
