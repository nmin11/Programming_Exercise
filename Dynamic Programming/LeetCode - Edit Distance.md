## **LeetCode > Dynamic Programming > Edit Distance**

</br>

[연습 문제 링크](https://leetcode.com/problems/edit-distance/)

</br>

📚 내가 사용한 프로그래밍 언어 : Java  
🎢 난이도 : Hard

</br>

## 영어 지문

Given two strings word1 and word2, return the minimum number of operations required to convert word1 to word2.  
You have the following three operations permitted on a word:

- Insert a character
- Delete a character
- Replace a character

</br>

## 추가 사항

- 0 <= word1.length, word2.length <= 500
- word1 and word2 consist of lowercase English letters.

</br>

## 문제 요약

word1과 word2, 두 단어가 주어졌을 때, word1을 word2로 변환하는 최소 작업 수를 리턴하라.  
단어에 대해서는 다음 3가지 작업 중 하나를 진행할 수 있다.

- 문자 삽입
- 문자 삭제
- 문제 교체

</br>

## [승지니어 님의 풀이](https://www.youtube.com/watch?v=dY_dZohgVa8&ab_channel=%EC%8A%B9%EC%A7%80%EB%8B%88%EC%96%B4Sengineer)

```java
class Solution {
    public int minDistance(String word1, String word2) {
        int len1 = word1.length();
        int len2 = word2.length();
        int[][] d = new int[len1+1][len2+1];
        /*
        d[i][j]가 의미하는 것
        → word1의 i까지의 부분문자열을
        word2의 j까지의 부분문자열로 교체하기 위한
        최소 작업 수

        ex) abc, def
        → d[1][1] : 'a'를 'd'로 교체하는 작업의 수 = 1
        */

        //Initialize
        for (int i = 0; i <= len1; i++) {
            d[i][0] = i;
        }

        for (int j = 0; j <= len2; j++) {
            d[0][j] = j;
        }

        //Loop
        for (int i = 1; i <= len1; i++) {
            for (int j = 1; j <= len2; j++) {
                if (word1.charAt(i-1) == word2.charAt(j-1)) {
                    d[i][j] = d[i-1][j-1];
                } else {
                    d[i][j] = Math.min(d[i-1][j-1],
                                      Math.min(d[i-1][j],
                                              d[i][j-1])) + 1;
                }
            }
        }

        //Return
        return d[len1][len2];
    }
}
```

이 문제는 Dynamic Programming의 교과서적인 문제이며, 대학교 등에서 많이들 풀게 되는 문제라고 설명해주셨다.  
위키에서도 이 문제에 대한 설명이 자세히 나와있다고는 해주셨는데, 추후에 GeeksforGeeks를 이용해서 다시 정리해볼 생각이다.  
역시 DP 문제는 아직도 봐도봐도 모르겠다.  
계속해서 연관 문제들을 찾아보고 공부해봐야겠다.
