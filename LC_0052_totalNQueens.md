#### 52. N皇后 II
n 皇后问题研究的是如何将 n 个皇后放置在 n×n 的棋盘上，并且使皇后彼此之间不能相互攻击。



上图为 8 皇后问题的一种解法。

给定一个整数 n，返回 n 皇后不同的解决方案的数量。

#### 示例:

```
输入: 4
输出: 2
解释: 4 皇后问题存在如下两个不同的解法。
[
 [".Q..",  // 解法 1
  "...Q",
  "Q...",
  "..Q."],

 ["..Q.",  // 解法 2
  "Q...",
  "...Q",
  ".Q.."]
]
```

```Java
class Solution {
    int ans = 0;
    public int totalNQueens(int n) {
        int[][] board = new int[n][n];
        backtrack(board, 0);
        return ans;
    }

    public void backtrack(int[][] board, int row) {
        if (row == board.length) {
            ans++;
            return;
        }
        for (int i = 0; i < board[0].length; i++) {
            if (!isValid(board, row, i))
                continue;
            board[row][i] = 1;
            backtrack(board,row+1);
            board[row][i] = 0;
        }
    }

    public boolean isValid(int[][] board, int row, int col) {
        // 同一列
        for (int i = row; i >= 0; i--) {
            if (board[i][col] ==  1) return false;
        }

        // 左上
        for (int i = row, j = col; i >= 0 && j < board.length; i--, j++) {
            if (board[i][j] == 1) return false;
        }

        // 右上
        for (int i = row, j = col; i >= 0 && j >= 0; i--, j--) {
            if (board[i][j] == 1) return false;
        }
        return true;
    }
}
```