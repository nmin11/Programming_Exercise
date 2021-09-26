## **LeetCode > Dynamic Programming > Minimum Path Sum**

</br>

[연습 문제 링크](https://leetcode.com/problems/minimum-path-sum/submissions/)

</br>

📚 내가 사용한 프로그래밍 언어 : Java  
🎢 난이도 : Medium

</br>

## 영어 지문

Given a m x n grid filled with non-negative numbers, find a path from top left to bottom right, which minimizes the sum of all numbers along its path.  
**Note:** You can only move either down or right at any point in time.

</br>

## 추가 사항

- 1 <= m, n <= 200
- 0 <= grid[i][j] <= 100

</br>

## 문제 요약

m x n의 그리드에 음수가 아닌 정수들이 채워져 있다.  
왼쪽 위 끝에서 오른쪽 아래 끝까지 이동하면서, 만나는 숫자들을 모두 더한 값이 최소값이 되는 경로를 찾고, 그 최소 합을 리턴하라.  
**Note:** 이동은 아래나 오른쪽 방향으로만 이동할 수 있다.

</br>

## [승지니어 님의 풀이](https://www.youtube.com/watch?v=v49ZgvJf7Xk&ab_channel=%EC%8A%B9%EC%A7%80%EB%8B%88%EC%96%B4Sengineer)

```java
/*
(0,0)에서 (1,1)까지 가는 최소값을 계산할 때,
윗칸에도 최소값 저장, 왼쪽칸에도 최소값 저장
→ 둘 중 더 작은 값을 취하면 된다.
*/
class Solution {
    public int minPathSum(int[][] grid) {
        int[][] d = new int[grid.length][grid[0].length];
        d[0][0] = grid[0][0];

        for (int i = 0; i < grid.length; i++) {
            for (int j = 0; j < grid[0].length; j++) {
                if (i == 0 && j == 0) continue;

                int up = (i > 0) ? d[i-1][j] : Integer.MAX_VALUE;
                int left = (j > 0) ? d[i][j-1] : Integer.MAX_VALUE;
                d[i][j] = Math.min(left, up) + grid[i][j];
            }
        }

        return d[grid.length-1][grid[0].length-1];
    }
}
```

이제야 DP 문제가 어느 정도 눈에 들어오는 느낌이 든다.  
관련 문제들을 계속해서 보다보니, 어느 정도 정해진 공식 같은 게 있고, DP 문제들은 다 이 공식 안에서 돌고 돈다는 느낌을 받았다.  
물론 훨씬 더 어려운 DP 문제를 받게 되면 필히 멘붕하게 되겠지만, 이 정도 익숙해진 것만으로도 꽤나 큰 성과라고 생각한다.  
하지만 더 어렵고 복잡한 DP 문제에 대비하기 위해서 관련 문제들을 계속해서 더 찾아보고 공부해보자.
