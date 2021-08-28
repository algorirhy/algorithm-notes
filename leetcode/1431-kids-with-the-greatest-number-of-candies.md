# [拥有最多糖果的孩子](https://leetcode-cn.com/problems/kids-with-the-greatest-number-of-candies)

```java
class Solution {
    public List<Boolean> kidsWithCandies(int[] candies, int extraCandies) {
        int maxCandies = 0;
        List<Boolean> res = new ArrayList<>();
        for (int candy : candies) {
            maxCandies = Math.max(maxCandies, candy);
        }
        for (int candy : candies) {
            res.add(candy + extraCandies >= maxCandies);
        }
        return res;
    }
}
```

