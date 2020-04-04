# [搜索旋转排序数组 II](https://leetcode-cn.com/problems/search-in-rotated-sorted-array-ii/)

二分查找

```java
class Solution {
    public boolean search(int[] nums, int target) {
        if (nums == null || nums.length == 0) return false;
        int left = 0, right = nums.length - 1;
        while (left <= right) {
            int mid = left + (right - left) / 2;
            if (nums[mid] == target) return true;
            if (nums[left] == nums[mid]) {
                // 不清楚有序无序
                left++;
                continue;
            } else if (nums[left] < nums[mid]) {
                // 前半部分有序
                if (nums[left] <= target && target < nums[mid]) {
                    // target 在前半部分
                    right = mid - 1;
                } else {
                    left = mid + 1;
                }
            } else {
                // 后半部分有序
                if (nums[mid] < target && target <= nums[right]) {
                    // target 在后半部分
                    left = mid + 1;
                } else {
                    right = mid - 1;
                }
            }
        }
        return false;
    }
}
```

