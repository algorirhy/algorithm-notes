# [只出现一次的数字 III](https://leetcode-cn.com/problems/single-number-iii/)

```java
class Solution {
    public int[] singleNumbers(int[] nums) {
        int xor = 0;
        for (int num : nums) {
            xor ^= num;
        }
        // a & (-a) 可以获得a最低的非0位
        int mask = xor & (-xor);
        int[] res = new int[2];
        for (int num : nums) {
            if ((num & mask) == 0) {
                res[0] ^= num;
            } else {
                res[1] ^= num;
            }
        }
        return res;
    }
}
```

