# [移动零](https://leetcode-cn.com/problems/move-zeroes/)

### 方法一

```java
class Solution {
    public void moveZeroes(int[] nums) {
        int count = 0;
        int len = nums.length;
        for (int i = 0; i < len; i++) {
            if(nums[i] == 0){
                ++count;
                continue;
            }
            nums[i - count] = nums[i];
        }
        for (int j = len - count; j < len; j++) {
            nums[j] = 0;
        }
    }
}
```
### 方法二

```java
class Solution {
    public void moveZeroes(int[] nums) {
        int j = 0;
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] != 0) {
                nums[j] = nums[i];
                if (i != j) {
                    nums[i] = 0;
                }
                j++;
            }
        }
    }
}
```

