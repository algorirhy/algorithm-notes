# [旋转矩阵](https://leetcode-cn.com/problems/rotate-matrix-lcci/)

先上下交换，再按对角线交换。

```java
class Solution {
    public void rotate(int[][] matrix) {
        int N = matrix.length;
        for (int i = 0; i < N / 2; i++) {
            int[] tmp = matrix[i];
            matrix[i] = matrix[N - i - 1];
            matrix[N - i - 1] = tmp;
        }
        for (int i = 0; i < N; i++) {
            for (int j = i + 1; j < N; j++) {
                int tmp = matrix[i][j];
                matrix[i][j] = matrix[j][i];
                matrix[j][i] = tmp;
            }
        }
    }
}
```

