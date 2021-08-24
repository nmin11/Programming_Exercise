## **Programmers > 연습문제 > 소수 찾기**

</br>

[연습 문제 링크](https://programmers.co.kr/learn/courses/30/lessons/12921)

</br>

📚 내가 사용한 프로그래밍 언어 : Java  
🎢 난이도 : Level 1

</br>

## 문제 요약

1부터 입력받은 숫자 n 사이에 있는 소수의 개수를 반환하라.

</br>

## 추가 사항

- 2 <= n <= 1000000

</br>

## 다른 사람의 풀이

생각보다 어려운 문제임을 깨닫게 되었고, 30분 가량 삽질 코드를 작성하다가 그냥 [다른 분의 풀이](https://parkjye.tistory.com/43)를 참고하게 되었다.

```java
class Solution {
    public int solution(int n) {
        int answer = 0;
        int[] numbers = new int[n + 1];

        for (int i = 2; i <= n; i++) numbers[i] = i;

        for (int i = 2; i < n; i++) {
            if (numbers[i] == 0) continue;
            for (int j = 2 * i; j <= n; j += i) numbers[j] = 0;
        }

        for (int i = 0; i< numbers.length; i++) {
            if (numbers[i] != 0) answer++;
        }

        return answer;
    }
}
```

['에라토스테네스의 체'](https://ko.wikipedia.org/wiki/%EC%97%90%EB%9D%BC%ED%86%A0%EC%8A%A4%ED%85%8C%EB%84%A4%EC%8A%A4%EC%9D%98_%EC%B2%B4)를 활용한 코드이다.

</br>

![Sieve_of_Eratosthenes_animation](https://user-images.githubusercontent.com/75058239/130625322-3995136e-cec7-4865-9c04-401859cf7066.gif)

</br>

핵심 코드는 2중 반복문 쪽에 있다.  
'에라토스테네스의 체' 방식으로 2부터 소수의 배수들을 하나씩 지워나간다.  
이 때 지우는 방식은 배열 안에 값을 0으로 바꿔주는 것이다.  
이렇게 해서 소수들과 0들만 남게 된 배열을 마지막에 반복문을 활용해서 0이 아닌 값들을 가려내서 소수의 개수를 판별해내는 모습을 확인할 수 있었다.

</br>

## 소감

정말 배울 것도 많고 알아야 할 것도 많다는 생각이 든다.  
소수를 검증하는 로직은 이미 완전히 알고 있다고 생각했는데 그야말로 크나큰 오산이었다.  
기록에만 그치지 말고 여러 번 다시 확인해서 꼭 내 것으로 만들자.
