## **LeetCode > Depth-First Search > Number of Islands**

<br>

[연습 문제 링크](https://leetcode.com/problems/number-of-islands/)

<br>

📚 내가 사용한 프로그래밍 언어 : Java  
🎢 난이도 : Medium

<br>

## 영어 지문

Given an `m x n` 2D binary grid `grid` which represents a map of `'1'`s (land) and `'0'`s (water), return _the number of islands._

An **island** is surrounded by water and is formed by connecting adjacent lands horizontally or vertically.  
You may assume all four edges of the grid are all surrounded by water.

<br>

## 예시

**Input:** grid = [  
 ["1","1","1","1","0"],  
 ["1","1","0","1","0"],  
 ["1","1","0","0","0"],  
 ["0","0","0","0","0"]  
]  
**Output:** 1

<br>

**Input:** grid = [  
 ["1","1","0","0","0"],  
 ["1","1","0","0","0"],  
 ["0","0","1","0","0"],  
 ["0","0","0","1","1"]  
]  
**Output:** 3

<br>

## 추가 사항

- m == grid.length
- n == grid[i].length
- 1 <= m, n <= 300
- grid[i][j] is '0' or '1'.

<br>

## 문제 요약

m x n 형태의 2D 이진 그리드인 `grid`가 주어진다.  
이 그리드는 땅을 뜻하는 '1'과, 물을 뜻하는 '0'으로 표현된다.  
이 그리드에 있는 섬들의 개수를 리턴하라.

**섬** 은 물로 둘러싸여 있고, 인접한 땅들을 수평 또는 수직으로 연결하여 형성된다.  
그리드의 4개의 모서리들은 모두 물로 둘러싸여 있다고 가정해도 좋다.

<br>

## [승지니어 님의 풀이](https://youtu.be/36du-PpTazc)

```java
class Solution {
    public int numIslands(char[][] grid) {
        int numIslands = 0;
        if (grid == null || grid.length == 0 || grid[0].length == 0) {
            return numIslands;
        }

        for (int i = 0; i < grid.length; i++) {
            for (int j = 0; j < grid[0].length; j++) {
                if (grid[i][j] != '1') continue;

                numIslands++;
                dfs(grid, i, j);
            }
        }

        return numIslands;
    }

    public void dfs(char[][] grid, int i, int j) {
        grid[i][j] = '-';

        //left
        if (j - 1 >= 0 && grid[i][j - 1] == '1') {
            dfs(grid, i, j - 1);
        }

        //right
        if (j + 1 < grid[0].length && grid[i][j + 1] == '1') {
            dfs(grid, i, j + 1);
        }

        //up
        if (i - 1 >= 0 && grid[i - 1][j] == '1') {
            dfs(grid, i - 1, j);
        }

        //down
        if (i + 1 < grid.length && grid[i + 1][j] == '1') {
            dfs(grid, i + 1, j);
        }
    }
}
```

풀이 방법 자체는 참 직관적이고, 이해도 잘 되었다.  
다만 딱 한 가지 문제는 역시, 내가 이걸 직접 풀어낼 수 있느냐이다.  
추후에 문제를 초기화하여 다시 풀어보는 시간을 꼭 가지자.
