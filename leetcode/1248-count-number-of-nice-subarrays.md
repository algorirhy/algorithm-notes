# [统计「优美子数组」](https://leetcode-cn.com/problems/count-number-of-nice-subarrays)

```java
class Solution {
    public int numberOfSubarrays(int[] nums, int k) {
        int left = 0, right = 0, oddCnt = 0, res = 0;
        while (right < nums.length) {
            if ((nums[right++] & 1) == 1) {
                oddCnt++;
            }
            if (oddCnt == k) {
                int rightEvenCnt = 0;
                while (right < nums.length && (nums[right] & 1) == 0) {
                    right++;
                    rightEvenCnt++;
                }
                int leftEvenCnt = 0;
                while ((nums[left] & 1) == 0) {
                    left++;
                    leftEvenCnt++;
                }
                res += (leftEvenCnt + 1) * (rightEvenCnt + 1);
                left++;
                oddCnt--;
            }
        }
        return res;
    }
}
```

