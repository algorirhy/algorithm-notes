# [x 的平方根](https://leetcode-cn.com/problems/sqrtx/)

### 方法一

二分查找

```java
class Solution {
    public int mySqrt(int x) {
        // 对于一个非负数n，它的平方根不会大于 n / 2 + 1
        long left = 0, right = x / 2 + 1;
        while (left <= right) {
            long mid = left + (right - left) / 2;
            long power = mid * mid;
            if (power == x) {
                return (int)mid;
            } else if (power < x) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }
        // 注意返回 right
        return (int)right;
    }
}
```

### 方法二

牛顿法

```java
class Solution {
    public int mySqrt(int x) {
        long res = x;
        while (res * res > x) {
            res = (res + x / res) / 2;
        }
        return (int)res;
    }
}
```

