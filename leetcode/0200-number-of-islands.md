# [岛屿数量](https://leetcode-cn.com/problems/number-of-islands/)

```java
class Solution {

    public int numIslands(char[][] grid) {
        int res = 0;
        for (int i = 0; i < grid.length; i++) {
            for (int j = 0; j < grid[0].length; j++) {
                if (grid[i][j] == '1') {
                    res++;
                    sinkingIsland(grid, i, j);
                }
            }
        }
        return res;
    }

    private void sinkingIsland(char[][] grid, int i, int j) {
        if (i < 0 || j < 0 || i >= grid.length || j >= grid[0].length || grid[i][j] == '0') {
            return;
        }
        grid[i][j] = '0';
        sinkingIsland(grid, i - 1, j);
        sinkingIsland(grid, i + 1, j);
        sinkingIsland(grid, i, j - 1);
        sinkingIsland(grid, i, j + 1);
    }
}
```

