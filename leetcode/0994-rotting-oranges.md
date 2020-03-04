# [腐烂的橘子](https://leetcode-cn.com/problems/rotting-oranges/)

虚拟节点 + 广度优先搜索

```java
class Solution {
    int[] dr = new int[]{-1, 0, 1, 0};
    int[] dc = new int[]{0, -1, 0, 1};

    public int orangesRotting(int[][] grid) {
        int row = grid.length;
        int col = grid[0].length;
        Queue<Integer> queue = new ArrayDeque();
        Map<Integer, Integer> depth = new HashMap();

        for(int i = 0; i < row; i++){
            for(int j = 0; j < col; j++){
                if(grid[i][j] == 2){
                    int index = i * col + j;
                    queue.add(index);
                    depth.put(index, 0);
                }
            }
        }

        int res = 0;
        while(!queue.isEmpty()){
            int index = queue.remove();
            int r = index / col;
            int c = index % col;
            for(int i = 0 ; i < 4; i++){
                int nr = r + dr[i];
                int nc = c + dc[i];
                if(nr >= 0 && nr < row && nc >= 0 && nc < col && grid[nr][nc] == 1){
                    grid[nr][nc] = 2;
                    int new_index = nr * col + nc;
                    queue.add(new_index);
                    depth.put(new_index, depth.get(index)+1);
                    res = depth.get(new_index);
                }
            }
        }

        for(int[] r : grid){
            for(int v : r){
                if(v == 1)
                    return -1;
            }
        }     
        return res;
    }
}
```

