# [柱状图中最大的矩形](https://leetcode-cn.com/problems/largest-rectangle-in-histogram/)

### 方法一

暴力解法

```java
class Solution {
    public int largestRectangleArea(int[] heights) {
        int len = heights.length;
        if (len == 0) return 0;
        int res = 0;
        for (int i = 0; i < len; i++) {
            // 找左边最后 1 个大于等于 heights[i] 的下标
            int left = i;
            while (left > 0 && heights[left - 1] >= heights[i]) left--;
            // 找右边最后 1 个大于等于 heights[i] 的下标
            int right = i;
            while (right < len - 1 && heights[right + 1] >= heights[i]) right++;

            int width = right - left + 1;
            res = Math.max(res, width * heights[i]);
        }
        return res;
    }
}
```

### 方法二

单调栈

```java
class Solution {
    public int largestRectangleArea(int[] heights) {
        int len = heights.length;
        Deque<Integer> stack = new ArrayDeque<>();
        stack.push(-1);
        int res = 0;
        for (int i = 0; i < len; i++) {
            // 栈不为空且栈顶大于等于当前的高度
            while (stack.peek() != -1 && heights[i] < heights[stack.peek()]) {
                res = Math.max(res, heights[stack.pop()] * (i - stack.peek() - 1));
            }
            stack.push(i);
        }
        while (stack.peek() != -1) {
            res = Math.max(res, heights[stack.pop()] * (len - stack.peek() - 1));
        }
        return res;
    }
}
```

