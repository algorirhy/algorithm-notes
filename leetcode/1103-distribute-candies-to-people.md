# [分糖果 II](https://leetcode-cn.com/problems/distribute-candies-to-people/)

暴力法

```java
class Solution {
    public int[] distributeCandies(int candies, int num_people) {
        int[] res = new int[num_people];
        for (int i = 0; candies != 0; i++) {
            res[i % num_people] += Math.min(candies, i + 1);
            candies -= Math.min(candies, i + 1);
        }
        return res;
    }
}
```