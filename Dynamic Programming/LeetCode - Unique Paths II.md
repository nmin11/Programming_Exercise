## **LeetCode > Dynamic Programming > Unique Paths**

</br>

[연습 문제 링크](https://leetcode.com/problems/unique-paths-ii/)

</br>

📚 내가 사용한 프로그래밍 언어 : Java  
🎢 난이도 : Medium

</br>

## 영어 지문

A robot is located at the top-left corner of a m x n grid.  
The robot can only move either down or right at any point in time.  
The robot is trying to reach the bottom-right corner of the grid.  
Now consider if some obstacles are added to the grids.  
How many unique paths would there be?  
An obstacle and space is marked as 1 and 0 respectively in the grid.

</br>

## 추가 사항

- 1 <= m, n <= 100
- obstacleGrid[i][j] is 0 or 1.

</br>

## 문제 요약

m x n의 그리드에서 로봇은 맨 위, 맨 왼쪽에 있다.  
로봇은 아래나 오른쪽으로만 움직일 수 있다.  
로봇이 맨 아래, 맨 오른쪽에 도달하고자 한다.  
이번에는 그리드 중에 장애물이 섞여 있다.  
로봇이 장애물을 피하면서 그리드의 맨 아래, 맨 오른쪽에 도달할 수 있는 경우의 수는 몇 가지인가?

</br>

## [승지니어 님의 풀이](https://www.youtube.com/watch?v=W2eoNUgzFVs&ab_channel=%EC%8A%B9%EC%A7%80%EB%8B%88%EC%96%B4Sengineer)

```java
class Solution {
    public int uniquePathsWithObstacles(int[][] obstacleGrid) {
        /*
        d[i][j] = 0,0 → i,j 까지 경로의 개수
        return d[x][y];
        */
        int[][] o = obstacleGrid;
        int[][] d = new int[o.length][o[0].length];
        d[0][0] = 1;

        for (int i = 0; i < o.length; i++) {
            for (int j = 0; j < o[0].length; j++) {
                int cur = o[i][j];
                if (cur == 1) {
                    d[i][j] = 0;
                } else {
                    if (i > 0) d[i][j] += d[i - 1][j];
                    if (j > 0) d[i][j] += d[i][j - 1];
                }
            }
        }

        return d[o.length - 1][o[0].length - 1];
    }
}
```

이전에 살펴보았던 [Unique Paths](https://github.com/nmin11/Programming_Exercise/blob/main/Dynamic%20Programming/LeetCode%20-%20Unique%20Paths.md) 문제에서 장애물을 피하는 단순한 로직만 추가되었기에, 이해하는 데에 크게 어려움은 없었다.
