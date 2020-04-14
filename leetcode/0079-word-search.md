# [单词搜索](https://leetcode-cn.com/problems/word-search/)

回溯搜索

```java
class Solution {
    private boolean[][] visited;
    private int[][] direction = {{-1, 0}, {0, -1}, {0, 1}, {1, 0}};

    public boolean exist(char[][] board, String word) {
        int row = board.length;
        int col = board[0].length;
        visited = new boolean[row][col];
        for (int i = 0; i < row; i++) {
            for (int j = 0; j <col; j++) {
                if (word.charAt(0) == board[i][j] && backTrack(board, word, i, j, 0)) {
                    return true;
                }
            }
        }
        return false;
    }

    private boolean backTrack(char[][] board, String word, int i, int j, int index) {
        if (index == word.length()) return true;
        if (i < 0 || i >= board.length || j < 0 || j >= board[0].length || 
                    visited[i][j] || word.charAt(index) != board[i][j]) {
            return false;
        }
        visited[i][j] = true;
        for (int k = 0; k < 4; k++) {
            int newX = i + direction[k][0];
            int newY = j + direction[k][1];
            if(backTrack(board, word, newX, newY, index + 1)) {
                return true;
            }
        }
        visited[i][j] = false;
        return false;
    }
}
```

