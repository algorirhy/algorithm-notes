# [每日温度](https://leetcode-cn.com/problems/daily-temperatures/)

单调栈

```java
class Solution {
    public int[] dailyTemperatures(int[] T) {
        int[] res = new int[T.length];
        Deque<Integer> s = new ArrayDeque<>();
        for (int i = 0; i < T.length; i++) {
            while (!s.isEmpty() && T[i] > T[s.peek()]) {
                res[s.peek()] = i - s.peek();
                s.pop();
            }
            s.push(i);
        }
        return res;
    }
}
```

