#### 51. N 皇后
n 皇后问题研究的是如何将 n 个皇后放置在 n×n 的棋盘上，并且使皇后彼此之间不能相互攻击。



上图为 8 皇后问题的一种解法。

给定一个整数 n，返回所有不同的 n 皇后问题的解决方案。

每一种解法包含一个明确的 n 皇后问题的棋子放置方案，该方案中 'Q' 和 '.' 分别代表了皇后和空位。

 

#### 示例：

```
输入：4
输出：[
 [".Q..",  // 解法 1
  "...Q",
  "Q...",
  "..Q."],

 ["..Q.",  // 解法 2
  "Q...",
  "...Q",
  ".Q.."]
]
解释: 4 皇后问题存在两个不同的解法。
```


```Java
class Solution {
    public List<List<String>> solveNQueens(int n) {
        List<List<String>> ans = new LinkedList();
        char [][]board = new char[n][n];
        backtrack(board, 0, ans);
        return ans;
    }

    public void backtrack(char[][] board, int row, List<List<String>> ans) {
        if (row == board.length) {
            List<String> list = new LinkedList();
            int n = board.length;
            for (int i = 0; i < n; i++) {
                String str = "";
                for (int j = 0; j < n; j++) {
                    if (board[i][j] != 'Q')
                        str += '.';
                    else str += board[i][j];
                }
                list.add(str);
            }
            ans.add(new LinkedList(list));
            return;
        }
        for (int i = 0; i < board[0].length; i++) {
            if (!isValid(board, row, i))
                continue;
            board[row][i] = 'Q';
            backtrack(board,row+1, ans);
            board[row][i] = '.';
        }
    }

    public boolean isValid(char[][] board, int row, int col) {
        // 同一列
        for (int i = row; i >= 0; i--) {
            if (board[i][col] ==  'Q') return false;
        }

        // 左上
        for (int i = row, j = col; i >= 0 && j < board.length; i--, j++) {
            if (board[i][j] == 'Q') return false;
        }

        // 右上
        for (int i = row, j = col; i >= 0 && j >= 0; i--, j--) {
            if (board[i][j] == 'Q') return false;
        }
        return true;
    }
}
```