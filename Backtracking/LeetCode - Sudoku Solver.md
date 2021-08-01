## **LeetCode > Array / Backtracking / Matrix > Valid Parentheses**

</br>

[연습 문제 링크](https://leetcode.com/problems/sudoku-solver/)

</br>

:books: 내가 사용한 프로그래밍 언어 : Java  
:roller_coaster: 난이도 : Hard

</br>

## 영어 지문

Write a program to solve a Sudoku puzzle by filling the empty cells.  
A sudoku solution must satisfy all of the following rules:

1. Each of the digits 1-9 must occur exactly once in each row.
2. Each of the digits 1-9 must occur exactly once in each column.
3. Each of the digits 1-9 must occur exactly once in each of the 9 3x3 sub-boxes of the grid.

The '.' character indicates empty cells.

</br>

## 추가 사항

- board.length == 9
- board[i].length == 9
- board[i][j] is a digit or '.'
- It is **guaranteed** that the input board has only one solution.

</br>

## 문제 요약

스도쿠 퍼즐의 빈 칸을 채우기 위한 프로그램을 작성해라.  
스도쿠 솔루션은 아래의 조건들을 만족해야 한다.

1. 1-9의 숫자가 한 행에서 한번만 있어야 한다.
2. 1-9의 숫자가 한 열에서 한번만 있어야 한다.
3. 1-9의 숫자가 3x3 서브 그리드에서 한번만 있어야 한다.

'.'은 비어있는 셀을 뜻한다.

</br>

input으로 2차원 배열이 주어지는데, 이 배열의 요소로는 숫자나 '.'의 char 타입이 들어있다.  
output으로는 '.'에 스도쿠의 조건에 충족하는 숫자를 넣어서 똑같이 2차원 배열로 반환하라.

</br>

## [승지니어 님의 풀이](https://www.youtube.com/watch?v=XnB8ef1W6MI&ab_channel=%EC%8A%B9%EC%A7%80%EB%8B%88%EC%96%B4Sengineer)

```java
class Solution {
    //백트래킹
    //정답을 찾을 때까지
    //  모든 경우의 수를 전진하면서, 스도쿠 유효성을 어기지 않는지 확인하면서 탐색
    //  더이상 나아갈 길이 없느면
    //  한칸 뒤로 후퇴
    public void solveSudoku(char[][] board) {
        backtrack(board, 0);
    }

    public boolean backtrack(char[][] board, int idx) {
        if (idx == 81) return true;
        int row = idx / 9;
        int col = idx % 9;
        char cur = board[row][col];
        if (cur != '.') {
            return backtrack(board, idx + 1);
        } else {
            for (int i = 1; i <= 9; i++) {
                board[row][col] = Integer.toString(i).charAt(0);
                if (isValidSudoku(board)) {
                    boolean b = backtrack(board, idx + 1);
                    if (b) return b;
                }
            }
            board[row][col] = '.';
            return false;
        }
    }

    public boolean isValidSudoku(char[][] board) {
        boolean[] b = new boolean[9];
        //가로, 세로, 섭그리드
        for (int i = 0; i < 3; i++) {
            //한줄의 규칙
            for (int j = 0; j < 9; j++) {
                Arrays.fill(b, false);
                for (int k = 0; k < 9; k++) {
                    char cur = '.';
                    if (i == 0) {
                        //가로
                        cur = board[j][k];
                    } else if (i == 1) {
                        //세로
                        cur = board[k][j];
                    } else {
                        //섭그리드
                        cur = board[j / 3 * 3 + k / 3][j % 3 * 3 + k % 3];
                    }
                    if (cur == '.') continue;
                    int val = Character.getNumericValue(cur);
                    if (b[val - 1]) return false;
                    b[val - 1] = true;
                }
            }
        }
        return true;
    }
}
```

제일 처음 0부터 인덱스부터 80까지 진행하면서 스도쿠의 빈 칸을 채운다.  
81에 도달하면 빈 칸을 모두 채웠으므로 리턴한다.  
81에 도달하지 못하면 backtracking을 하면서 빈 칸을 채워나가는 방식이다.

</br>

[스도쿠 검증 문제](https://www.youtube.com/watch?v=GjqMAoUeh1Q&ab_channel=%EC%8A%B9%EC%A7%80%EB%8B%88%EC%96%B4Sengineer)에서 이미 스도쿠를 검증하는 로직을 짰었기에, 이를 그대로 활용했다.  
스도쿠를 검증하면서 모든 경우의 수를 탐색하면서 모든 정답을 찾아내는 방식이다.  
그리고 정답을 찾았을 때, 재귀 탐색을 그만하고 정답 상태의 2차원 배열을 반환한다.

</br>

## 소감

Backtracking 기법을 아직 모르는 입장에서 나에겐 아직 섣부른 느낌이 있었다.  
반드시 Backtracking에 대한 추가적인 공부를 하고 다시 정리를 해봐야겠다.
