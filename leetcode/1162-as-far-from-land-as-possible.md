# [地图分析](https://leetcode-cn.com/problems/as-far-from-land-as-possible/)

```java
class Solution {
    public int maxDistance(int[][] grid) {
        int N = grid.length;
        int[] dx = {-1, 1, 0, 0};
        int[] dy = {0, 0, -1, 1};

        Deque<int[]> queue = new ArrayDeque<>();
        for (int i = 0; i < N; i++) {
            for (int j = 0; j < N; j++) {
                if (grid[i][j] == 1) {
                    queue.offer(new int[]{i, j});
                }
            }
        }
        int size = queue.size();
        if (size == 0 || size == N * N) {
            return -1;
        }

        int[] point = null;
        while (!queue.isEmpty()) {
            point = queue.poll();
            int x = point[0], y = point[1];
            for (int k = 0; k < 4; k++) {
                int newX = x + dx[k];
                int newY = y + dy[k];
                if (newX < 0 || newX >= N || newY < 0 || newY >= N || grid[newX][newY] != 0) {
                    continue;
                }
                // 层数 + 1
                grid[newX][newY] = grid[x][y] + 1;
                queue.offer(new int[]{newX, newY});
            }
        }

        // 最后访问的点
        return grid[point[0]][point[1]] - 1;
    }
}
```

