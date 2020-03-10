# [最长上升子序列](https://leetcode-cn.com/problems/longest-increasing-subsequence/)

### 方法一

动态规划

```java
class Solution {
    public int lengthOfLIS(int[] nums) {
        int res = 0;
        int len = nums.length;
        if (len < 2) return len;
        int[] dp = new int[len];
        Arrays.fill(dp, 1);
        for (int i = 1; i < len; i++) {
            for (int j = 0; j < i; j++) {
                if (nums[j] < nums[i]) {
                    dp[i] = Math.max(dp[i], dp[j] + 1);
                }
            }
            res = Math.max(res, dp[i]);
        }
        retun res;
    }
}
```

### 方法二

动态规划 + 贪心算法 + 二分查找，有点难理解。

```java
class Solution {
    public int lengthOfLIS(int[] nums) {
        int res = 0;
        int len = nums.length;
        if (len < 2) return len;
        int[] tail = new int[len];
        tail[0] = nums[0];
        int end = 0;
        for (int i = 1; i < len; i++) {
            if (nums[i] > tail[end]) {
                end++;
                tail[end] = nums[i];
            } else {
                int left = 0, right = end;
                while (left < right) {
                    int mid = left + ((right - left) >>> 1);
                    if (tail[mid] < nums[i]) {
                        left = mid + 1;
                    } else {
                        right = mid;
                    }
                }
                tail[left] = nums[i];
            }
        }
        return ++end;
    }
}
```

