# [第 k 个数](https://leetcode-cn.com/problems/get-kth-magic-number-lcci/)

```java
class Solution {
    public int getKthMagicNumber(int k) {
        int p3 = 0, p5 = 0, p7 = 0;
        int[] nums = new int[k];
        nums[0] = 1;
        for (int i = 1; i < k; i++) {
            nums[i] = Math.min(Math.min(nums[p3] * 3, nums[p5] * 5), nums[p7] * 7);
            if (nums[i] == nums[p3] * 3) p3++;
            if (nums[i] == nums[p5] * 5) p5++;
            if (nums[i] == nums[p7] * 7) p7++;
        }
        return nums[k - 1];
    }
}
```

