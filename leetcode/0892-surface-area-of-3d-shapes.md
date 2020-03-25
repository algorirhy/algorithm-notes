# [三维形体的表面积](https://leetcode-cn.com/problems/surface-area-of-3d-shapes/)

### 方法一

做减法

```java
class Solution {
    public int surfaceArea(int[][] grid) {
        int N = grid.length;
        // 立方体数量 接触面数量
        int cubes = 0, faces = 0;
        for (int i = 0; i < N; i++) {
            for (int j =0; j < N; j++) {
                cubes += grid[i][j];
                if (grid[i][j] > 0) {
                    // 叠起来的 v 个立方体有 v-1 个接触面
                    faces += grid[i][j] - 1;
                }
                if (i > 0) {
                    // 当前柱子与后面柱子的接触面数量
                    faces += Math.min(grid[i - 1][j], grid[i][j]);
                }
                if (j > 0) {
                    // 当前柱子与左边柱子的接触面数量
                    faces += Math.min(grid[i][j - 1], grid[i][j]);
                }
            }
        }
        return cubes * 6 - faces * 2;
    }
}
```

###  方法二

做加法

```java
class Solution {
    public int surfaceArea(int[][] grid) {
        int N = grid.length;
        int res = 0;
        for (int i = 0; i < N; i++) {
            for (int j = 0; j < N; j++) {
                // 后面露出的表面积
                res += (i > 0) ? Math.max(grid[i][j] - grid[i - 1][j], 0) : grid[i][j];
                // 前面露出的表面积
                res += (i < N - 1) ? Math.max(grid[i][j] - grid[i + 1][j], 0) : grid[i][j];
                // 左边露出的表面积
                res += (j > 0) ? Math.max(grid[i][j] - grid[i][j - 1], 0) : grid[i][j];
                // 右边露出的表面积
                res += (j < N - 1) ? Math.max(grid[i][j] - grid[i][j + 1], 0) : grid[i][j];
                // 顶部、底部的表面积
                res += grid[i][j] > 0 ? 2 : 0;
            }
        }
        return res;
    }
}
```

