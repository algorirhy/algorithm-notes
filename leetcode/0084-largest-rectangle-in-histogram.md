# [柱状图中最大的矩形](https://leetcode-cn.com/problems/largest-rectangle-in-histogram/)

### 方法一

暴力解法

S = heights[i] * (right - left + 1)；

left：左边最后一个大于等于 heights[i] 的下标

right：找右边最后一个大于等于 heights[i] 的下标

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

S = heights[i] * (right - left - 1)；

left：左边第一个小于 heights[i] 的下标

right：找右边第一个小于 heights[i] 的下标

```java
class Solution {
    public int largestRectangleArea(int[] heights) {
        int res = 0;
        int len = heights.length;
        Deque<Integer> s = new ArrayDeque<>();
        // 哨兵
        s.push(-1);
        for (int i = 0; i < len; i++) {
            // 栈不为空且 heights[i] 小于栈顶高度
            while (s.peek() != -1 && heights[i] < heights[s.peek()]) {
                // s.peek(), heights[i] 分别是 s.pop() 的左右边界
                res = Math.max(res, heights[s.pop()] * (i - s.peek() - 1));
            }
            s.push(i);
        }
        while (s.peek() != -1) {
            res = Math.max(res, heights[s.pop()] * (len - s.peek() - 1));
        }
        return res;
    }
}
```

