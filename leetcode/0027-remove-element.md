# [移除元素](https://leetcode-cn.com/problems/remove-element/)

### 方法一

```java
class Solution {
    public int removeElement(int[] nums, int val) {
        int res = 0;
        for (int num : nums) {
            if (num != val) {
                nums[res++] = num;
            }
        }
        return res;
    }
}
```

### 方法二

```java
class Solution {
    public int removeElement(int[] nums, int val) {
        int res = nums.length;
        for (int i = 0; i < res; ) {
            if (nums[i] == val) {
                nums[i] = nums[--res];
            } else {
                i++;
            }
        }
        return res;
    }
}
```

