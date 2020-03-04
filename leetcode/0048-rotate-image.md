# [旋转图像](https://leetcode-cn.com/problems/rotate-image/submissions/)

### 方法一

每次交换四个点

```java
class Solution {
    public void rotate(int[][] matrix) {
        int n = matrix.length;
        for(int i = 0; i < n/2; i++){
            for(int j = i; j < n-i-1; j++){
                int tmp = matrix[i][j];
                matrix[i][j] = matrix[n-j-1][i];
                matrix[n-j-1][i] = matrix[n-i-1][n-j-1];
                matrix[n-i-1][n-j-1] = matrix[j][n-i-1];
                matrix[j][n-i-1] = tmp;
            }
        }
    }
}
```

### 方法二

先上下翻转，再正对角线翻转

```java
class Solution {
    public void rotate(int[][] matrix) {
        int n = matrix.length;
        for(int i = 0; i < n/2; i++){
            int[] tmp = matrix[i];
            matrix[i] = matrix[n-i-1];
            matrix[n-i-1] = tmp;
        }
        for(int i = 0; i < n; i++){
            for(int j = i+1; j < n; j++){
                int tmp = matrix[i][j];
                matrix[i][j]= matrix[j][i];
                matrix[j][i] = tmp;
            }
        }
    }
}
```

