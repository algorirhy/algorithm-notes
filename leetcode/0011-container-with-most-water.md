# [盛最多水的容器](https://leetcode-cn.com/problems/container-with-most-water/)

双指针

```java
class Solution {
    public int maxArea(int[] height) {
        int i = 0, j = height.length - 1, res = 0;
        while(i < j){
            int minHeight = height[i] < height[j] ? height[i++] : height[j--];
            int area = (j - i + 1) * minHeight;
            res = Math.max(res, area);
        }
        return res;
    }
}
```

