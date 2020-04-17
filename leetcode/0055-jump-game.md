# [跳跃游戏](https://leetcode-cn.com/problems/jump-game/)

逆推

```java
class Solution {
    public boolean canJump(int[] nums) {
        int pos = nums.length - 1;
        for (int i = nums.length - 2; i >= 0; i--) {
            if (i + nums[i] >= pos) {
                pos = i;
            }
        }
        return pos == 0;
    }
}
```

