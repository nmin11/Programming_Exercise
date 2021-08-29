## **LeetCode > Dynamic Programming / Combinatorics > Unique Paths**

</br>

[연습 문제 링크](https://leetcode.com/problems/unique-paths/)

</br>

📚 내가 사용한 프로그래밍 언어 : Java  
🎢 난이도 : Medium

</br>

## 영어 지문

A robot is located at the top-left corner of a m x n grid.  
The robot can only move either down or right at any point in time.  
The robot is trying to reach the bottom-right corner of the grid.  
How many possible unique paths are there?

</br>

## 추가 사항

- 1 <= m, n <= 100
- It's guaranteed that the answer will be less than or equal to 2 \* 10⁹.

</br>

## 문제 요약

m x n의 그리드에서 로봇은 맨 위, 맨 왼쪽에 있다.  
로봇은 아래나 오른쪽으로만 움직일 수 있다.  
로봇이 맨 아래, 맨 오른쪽에 도달하고자 할 때, 몇 가지 경우의 수가 존재하는가?

</br>

## 승지니어 님의 풀이

```java
class Solution {
    public int uniquePaths(int m, int n) {
        int[][] d = new int[m][n];
        d[0][0] = 1;

        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (i > 0) d[i][j] += d[i - 1][j];
                if (j > 0) d[i][j] += d[i][j - 1];
            }
        }

        return d[m - 1][n - 1];
    }
}
```

승지니어 님께서 점화식을 이용한 풀이라고 말씀해주셨다.  
만약 그리드가 0x0 이라면 경우의 수는 1이므로 초기값을 1로 지정해준다.  
그리고 0x0에서 1x1에 도달하는 방법을 예시로 살펴보자면, 경우의 수는 0x1에서 내려오거나, 1x0에서 오른쪽으로 이동하거나 할 것이다.  
이를 점화식으로 다시 생각해보자면, **'1x1에 도달하는 방법의 개수'** 는 **'0x1까지 도달할 수 있었던 방법의 개수 + 1x0까지 도달할 수 있었던 방법의 개수'** 이다.
