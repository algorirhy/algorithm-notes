# [单词搜索](https://leetcode-cn.com/problems/word-search/)

回溯搜索

```java
class Solution {
    private int row, col;
    private String word;
    private char[][] board;
    private boolean[][] visited;
    private int[][] direction = {{-1, 0}, {0, -1}, {0, 1}, {1, 0}};

    public boolean exist(char[][] board, String word) {
        this.word = word;
        this.board = board;
        row = board.length;
        col = board[0].length;
        visited = new boolean[row][col];
        for (int i = 0; i < row; i++) {
            for (int j = 0; j <col; j++) {
                if (word.charAt(0) == board[i][j] && dfs(i, j, 0)) {
                    return true;
                }
            }
        }
        return false;
    }

    private boolean dfs(int i, int j, int index) {
        if (index == word.length()) return true;
        if (i < 0 || i >= row || j < 0 || j >= col || visited[i][j]
                || word.charAt(index) != board[i][j]) {
            return false;
        }
        visited[i][j] = true;
        for (int k = 0; k < 4; k++) {
            int newX = i + direction[k][0];
            int newY = j + direction[k][1];
            if(dfs(newX, newY, index + 1)) {
                return true;
            }
        }
        visited[i][j] = false;
        return false;
    }
}
```

