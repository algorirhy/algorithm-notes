# [N皇后](https://leetcode-cn.com/problems/n-queens/)

```java
class Solution {
    private List<List<String>> res;

    public List<List<String>> solveNQueens(int n) {
        res = new LinkedList<>();
        char[][] board = new char[n][n];
        for (char[] ch : board) {
            Arrays.fill(ch, '.');
        }
        backtrack(board, 0);
        return res;
    }

    private void backtrack(char[][] board, int row) {
        if (row == board.length) {
            res.add(toStringList(board));
            return;
        }
        for (int col = 0; col < board.length; col++) {
            if (isValid(board, row, col)) {
                board[row][col] = 'Q';
                backtrack(board, row + 1);
                board[row][col] = '.';
            }
        }
    }

    private boolean isValid(char[][] board, int row, int col) {
        // 检查列是否有皇后互相冲突
        for (char[] ch : board) {
            if (ch[col] == 'Q') {
                return false;
            }
        }
        // 检查右上方是否有皇后互相冲突
        for (int i = row - 1, j = col + 1; i >= 0 && j < board.length; i--, j++) {
            if (board[i][j] == 'Q') {
                return false;
            }
        }
        // 检查左上方是否有皇后互相冲突
        for (int i = row - 1, j = col - 1; i >= 0 && j >= 0; i--, j--) {
            if (board[i][j] == 'Q') {
                return false;
            }
        }
        return true;
    }

    private List<String> toStringList(char[][] board) {
        List<String> res = new LinkedList<>();
        for (char[] ch : board) {
            res.add(String.valueOf(ch));
        }
        return res;
    }
}
```

