# [合并排序的数组](https://leetcode-cn.com/problems/sorted-merge-lcci/)

```java
class Solution {
    public void merge(int[] A, int m, int[] B, int n) {
        while(m > 0 && n > 0){
            //A[m+n-1] = A[m-1] > B[n-1] ? A[m-- - 1] : B[n-- - 1];
            if(A[m-1] > B[n-1]){
                A[m+n-1] = A[m-1];
                m--;
            }else{
                A[m+n-1] = B[n-1];
                n--;
            }
        }
        while(n > 0){
            A[n-1] = B[n-1];
            n--;
        }
    }
}
```

