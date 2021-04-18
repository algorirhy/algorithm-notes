# [删除排序数组中的重复项](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-array/)

双指针

## Java

```java
class Solution {
    public int removeDuplicates(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }
        int p = 0, q = 1;
        while (q < nums.length) {
            if (nums[p] != nums[q]) {
                if (q - p > 1) {
                    nums[p + 1] = nums[q];
                }
                p++;
            }
            q++;
        }
        return p + 1;
    }
}
```

## Go

```go
func removeDuplicates(nums []int) int {
    if len(nums) < 2 {
        return len(nums)
    }
    slow := 0
    for fast := 1; fast < len(nums); fast++ {
        if nums[fast] != nums[slow] {
            slow++
            nums[slow] = nums[fast]
        }
    }
    return slow+1
}
```
