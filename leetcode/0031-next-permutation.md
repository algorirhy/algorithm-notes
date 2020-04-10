# [下一个排列](https://leetcode-cn.com/problems/next-permutation/)

```java
class Solution {
    public void nextPermutation(int[] nums) {
        int len = nums.length;
        int index = -1;
         // 从后往前扫描找到第一个下标i使得nums[i] < nums[i + 1]
        for (int i = len - 2; i>= 0; i--) {
            if (nums[i] < nums[i + 1]) {
                index = i;
                break;
            }
        }
        if (index != -1) {
            // 从后往前扫描找到找到第一个下标j使得nums[i] > nums[index]
            for (int i = len - 1; i > index; i--) {
                if (nums[i] > nums[index]) {
                    swap(nums, i, index);
                    break;
                }
            }
        }
        reverse(nums, index + 1, len - 1);
    }

    private void reverse(int[] nums, int start, int end) {
        while (start < end) {
            swap(nums, start++, end--);
        }
    }

    private void swap(int[] nums, int i, int j) {
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }
}
```

