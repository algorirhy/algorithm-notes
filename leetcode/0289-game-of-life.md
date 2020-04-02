# [生命游戏](https://leetcode-cn.com/problems/game-of-life/)

```java
class Solution {
    public void gameOfLife(int[][] board) {
        int[] dx = {0, 0, 1, 1, 1, -1, -1, -1};
        int[] dy = {1, -1, 1, -1, 0, 1, -1, 0};
        // 第一次遍历，标记中间值
        for (int i = 0; i < board.length; i++) {
            for (int j = 0; j < board[0].length; j++) {
                int x, y, live = 0;
                for (int k = 0; k < 8; k++) {
                    x = i + dx[k];
                    y = j + dy[k];
                    if (x < 0 || x >= board.length || y < 0 || y >= board[0].length) {
                        continue;
                    }
                    // 最开始是活的细胞
                    if (board[x][y] == 1 || board[x][y] == 2) {
                        live++;
                    }
                }
                // 如果死细胞要复活，用中间值 -1 记录
                if (board[i][j] == 0) {
                    if (live == 3) {
                        board[i][j] = -1;
                    }
                } else {
                    // 如果活细胞将死亡，用中间值 2 来记录
                    if (live < 2 || live > 3) {
                        board[i][j] = 2;
                    }
                }
            }
        }
        // 第二次遍历，去掉中间值
        for (int i = 0; i < board.length; i++) {
            for (int j = 0; j < board[0].length; j++) {
                if (board[i][j] == 2) {
                    board[i][j] = 0;
                } else if (board[i][j] == -1) {
                    board[i][j] = 1;
                }
            }
        }
    }
}
```

