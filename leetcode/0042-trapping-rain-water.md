# [接雨水](https://leetcode-cn.com/problems/trapping-rain-water/)

一个位置能容下的雨水量等于它左右两边柱子最大高度的最小值减去它的高度

min(left_max, right_max) - height[i]

### 方法一

双指针

```java
class Solution {
    public int trap(int[] height) {
        int res = 0;
        int left = 0, right = height.length - 1;
        int leftMax = 0, rightMax = 0;
        while (left < right) {
            if (height[left] < height[right]) {
                // 左边较低
                if (height[left] >= leftMax) {
                    // 更新左最大值
                    leftMax = height[left++];
                } else {
                    // 计算高度差
                    res += leftMax - height[left++];
                }
            } else {
                if (height[right] >= rightMax) {
                    rightMax = height[right--];
                } else {
                    res += rightMax - height[right--];
                }
            }
        }
        return res;
    }
}
```

### 方法二

单调栈

```java
class Solution {
    public int trap(int[] height) {
        int res = 0, curIndex = 0;
        Deque<Integer> s = new ArrayDeque<>();
        while (curIndex < height.length) {
            // 栈不为空且当前高度大于栈顶高度
            while (!s.isEmpty() && height[curIndex] > height[s.peek()]) {
                int top = s.pop();
                if (s.isEmpty()) break;
                int distance = curIndex - s.peek() - 1;
                // 左右高度的较小值与当前位置的高度差
                int heightDiff = Math.min(height[s.peek()], height[curIndex]) - height[top];
                res += distance * heightDiff;
            }
            s.push(curIndex++);
        }
        return res;
    }
}
```
