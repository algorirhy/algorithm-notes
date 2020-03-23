# [在排序数组中查找元素的第一个和最后一个位置](https://leetcode-cn.com/problems/find-first-and-last-position-of-element-in-sorted-array/)

### 方法一

```java
class Solution {
    public int[] searchRange(int[] nums, int target) {
        int left = binarySearch(nums, target - 0.5);
        int right =  binarySearch(nums, target + 0.5);
        if (left == right) {
            return new int[]{-1, -1};
        }
        return new int[]{left, right - 1};
    }

    private int binarySearch(int[] nums, double target) {
        int left = 0, right = nums.length - 1;
        while (left <= right) {
            int mid = (right + left) >>> 1;
            if (nums[mid] < target) {
                left = mid + 1;
            } else if (nums[mid] > target) {
                right = mid - 1;
            }
        }
        return left;
    }
}
```

### 方法二

```java
class Solution {
    public int[] searchRange(int[] nums, int target) {
        int left = leftBound(nums, target);
        int right =  rightBound(nums, target);
        if (left > right) {
            return new int[]{-1, -1};
        }
        return new int[]{left, right};
    }

    // 第一次出现的下标或者第一个比target大的下标
    private int leftBound(int[] nums, int target) {
        int left = 0, right = nums.length - 1;
        while (left <= right) {
            int mid = (left + right) >>> 1;
            if (nums[mid] < target) {
                left = mid + 1;
            } else if (nums[mid] >= target) {
                right = mid - 1;
            }
        }
        return left;
    }

    // 最后一次出现的下标或者第一个比target小的下标
    private int rightBound(int[] nums, int target) {
        int left = 0, right = nums.length - 1;
        while (left <= right) {
            int mid = (left + right) >>> 1;
            if (nums[mid] <= target) {
                left = mid + 1;
            } else if (nums[mid] > target) {
                right = mid - 1;
            }
        }
        return right;
    }
}
```

