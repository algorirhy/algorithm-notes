# [矩形面积](https://leetcode-cn.com/problems/rectangle-area/)

```java
class Solution {
    public int computeArea(int A, int B, int C, int D, int E, int F, int G, int H) {
        int area = (D - B) * (C - A) + (H - F) * (G - E);
        if (D <= F || C <= E || B >= H || A >= G) {
            return area;
        }
        int left = Math.max(A, E);
        int right = Math.min(C, G);
        int up = Math.min(D, H);
        int down = Math.max(B, F);
        return area - (right - left) * (up - down);
    }
}
```

