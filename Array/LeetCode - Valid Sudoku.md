## **LeetCode > Array / Hash Table / Matrix > Valid Parentheses**

</br>

[연습 문제 링크](https://leetcode.com/problems/valid-sudoku/)

</br>

:books: 내가 사용한 프로그래밍 언어 : Java  
:roller_coaster: 난이도 : Medium

</br>

## 영어 지문

Determine if a 9 x 9 Sudoku board is valid. Only the filled cells need to be validated according to the following rules:

1. Each row must contain the digits 1-9 without repetition.
2. Each column must contain the digits 1-9 without repetition.
3. Each of the nine 3 x 3 sub-boxes of the grid must contain the digits 1-9 without repetition.

Note

- A Sudoku board (partially filled) could be valid but is not necessarily solvable.
- Only the filled cells need to be validated according to the mentioned rules.

</br>

## 문제 요약

주어진 스도쿠 배열의 유효성이 맞는지 검사해라.  
채워진 셀들에 한해서만 검증하면 된다.  
주어진 덜 채워진 스도쿠 배열은 이미 유효성이 깨졌는지에 대해 검증될 수 있지만 문제를 풀 필요는 없다.

</br>

## 추가 사항

- board.length == 9
- board[i].length == 9
- board[i][j] is a digit or '.'

## [승지니어 님의 풀이](https://www.youtube.com/watch?v=GjqMAoUeh1Q&t=457s&ab_channel=%EC%8A%B9%EC%A7%80%EB%8B%88%EC%96%B4Sengineer)

```java
class Solution {
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

일전에 코드스테이츠 Toy 문제에서 스도쿠 빈 칸을 채우는 어려운 문제를 맞닥뜨렸기에 유튜브에서 이 문제를 보면서 풀이를 참조했다.  
스도쿠 문제가 정말 어려웠는데 확실히 이 영상을 한 번 보고나니 조금은 쉽게 다가오는 느낌이다.  
이 문제의 풀이를 참고해서 얼렁뚱땅 넘어갔던 코드스테이츠의 스도쿠 문제도 다시 한번 확인해봐야겠다.  
하지만 저 board[j / 3 \* 3 + k / 3][j % 3 * 3 + k % 3] 부분은 사실 아직 좀 이해가 되지 않는다.  
좀 더 노려봐야겠다. :eyes:
