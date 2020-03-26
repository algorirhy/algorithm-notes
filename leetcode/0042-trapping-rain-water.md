# [接雨水](https://leetcode-cn.com/problems/trapping-rain-water/)

一个位置能容下的雨水量等于它左右两边柱子最大高度的最小值减去它的高度

min(left_max, right_max) - height[i]

### 方法一

双指针

```java
class Solution {
    public int trap(int[] height) {
        int res = 0;
        int len = height.length;
        if (len == 0) return res;
        int left = 0, right = len - 1;
        int left_max = 0, right_max = 0;
        while (left < right) {
            if (height[left] < height[right]) {
                if (height[left] >= left_max) {
                    left_max = height[left];
                } else {
                    res += left_max - height[left];
                }
                left++;              
            } else {
                if (height[right] >= right_max) {
                    right_max = height[right];
                } else {
                    res += right_max - height[right];
                }
                right--;  
            }
        }
        return res;
    }
}
```

### 方法二

利用栈

```java
class Solution {
    public int trap(int[] height) {
        int res = 0, cur = 0;
        int len = height.length;
        if (len == 0) return res;
        Deque<Integer> s = new ArrayDeque<>();
        while (cur < len) {
            while (!s.isEmpty() && height[cur] > height[s.peek()]) {
                int top = s.pop();
                if (s.isEmpty()) break;
                int distance = cur - s.peek() - 1;
                // 左右高度的较小值与当前位置的高度差
                int bound_height = Math.min(height[cur], height[s.peek()]) - height[top];
                res += distance * bound_height;
            }
            s.push(cur++);
        }
        return res;
    }
}
```
