# [跳跃游戏 II](https://leetcode-cn.com/problems/jump-game-ii/)

贪心

```java
class Solution {
    public int jump(int[] nums) {
        // 当前能跳的边界
        int end = 0;
        int maxPosition = 0;
        int steps = 0;
        for (int i = 0; i < nums.length - 1; i++) {
            // 找能跳的最远的
            maxPosition = Math.max(maxPosition, nums[i] + i);
            if (i == end) {
                end = maxPosition;
                steps++;
            }
        }
        return steps;
    }
}
```

