# [岛屿数量](https://leetcode-cn.com/problems/number-of-islands/)

```java
class Solution {
    int[] dx = {0, 0, -1, 1};
    int[] dy = {-1, 1, 0, 0};

    public int numIslands(char[][] grid) {
        int res = 0;
        for (int i = 0; i < grid.length; i++) {
            for (int j = 0; j < grid[0].length; j++) {
                if (grid[i][j] == '1') {
                    res++;
                    sinkIsland(grid, i, j);
                }
            }
        }
        return res;
    }

    private void sinkIsland(char[][] grid, int x, int y) {
        grid[x][y] = '0';
        for (int i = 0; i < 4; i++) {
            int newX = x + dx[i];
            int newY = y + dy[i];
            if (newX >= 0 && newX < grid.length && newY >= 0 && 
                        newY < grid[0].length && grid[newX][newY] == '1') {
                sinkIsland(grid, newX, newY);
            }
        }
    }
}
```

