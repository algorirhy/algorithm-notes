# [岛屿的最大面积](https://leetcode-cn.com/problems/max-area-of-island/)

沉岛思想

```java
class Solution {
    public int maxAreaOfIsland(int[][] grid) {
        int res = 0;
        for (int i = 0; i < grid.length; i++) {
            for (int j = 0; j < grid[i].length; j++) {
                if (grid[i][j] == 1) {
                    res = Math.max(res, dfs(grid, i, j));
                }
            }
        }
        return res;
    }

    private int dfs(int[][] grid, int i, int j) {
        if (i < 0 || j < 0 || i >= grid.length || j >= grid[i].length || grid[i][j] == 0) {
            return 0;
        }
        //沉岛思想
        grid[i][j] = 0;
        int num = 1;
        num += dfs(grid, i - 1, j);
        num += dfs(grid, i + 1, j);
        num += dfs(grid, i, j - 1);
        num += dfs(grid, i, j + 1);
        return num;
    }
}
```

