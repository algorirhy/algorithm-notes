# [寻找重复数](https://leetcode-cn.com/problems/find-the-duplicate-number)

二分查找

```java
class Solution {
    public int findDuplicate(int[] nums) {
        int len = nums.length;
        int left = 1, right = len - 1;
        while (left < right) {
            int mid = (left + right) >>> 1;
            int cnt = 0;
            for (int num : nums) {
                if (num <= mid) {
                    cnt++;
                }
            }
            if (cnt > mid) {
                right = mid;
            } else {
                left = mid + 1;
            }
        }
        return left;
    }
}
```

