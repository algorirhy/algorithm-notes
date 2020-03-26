# [分割数组的最大值](https://leetcode-cn.com/problems/split-array-largest-sum/)

```java
class Solution {
    public int splitArray(int[] nums, int m) {
        int left =0, right = 0;
        for (int num : nums) {
            left = Math.max(left, num);
            right += num;
        }
        if (m == 1) return right;
        while (left < right) {
            int mid = (left + right) >> 1;
            int cmp = check(nums, m, mid);
            if (cmp == -1) {
                right = mid - 1;
            } else if (cmp == 1) {
                left = mid + 1;
            } else {
                right = mid;
            }
        }
        return left;
    }

    private int check(int[] nums, int m, int step) {
        int sum = 0;
        int count = 1;
        for (int num : nums) {
            if (sum + num > step) {
                count++;
                sum = num;
            } else {
                sum += num;
            }
        }
        return Integer.compare(count, m);
    }
}
```

