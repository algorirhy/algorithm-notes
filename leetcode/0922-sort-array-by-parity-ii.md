# [按奇偶排序数组 II](https://leetcode-cn.com/problems/sort-array-by-parity-ii/)

双指针

```java
class Solution {
    public int[] sortArrayByParityII(int[] A) {
        int odd = 1;
        for (int even = 0; even < A.length; even += 2) {
            // 偶数位的数为奇数
            if (A[even] % 2 == 1) {
                // 寻找下一个奇数位为偶数的下标
                while (A[odd] % 2 == 1) {
                    odd += 2;
                }
                int tmp = A[even];
                A[even] = A[odd];
                A[odd] = tmp;
            }
        }
        return A;
    }
}
```

