# [卡牌分组](https://leetcode-cn.com/problems/x-of-a-kind-in-a-deck-of-cards/)

统计每个整数出现的次，然后求所有出现次数的最大公约数，如果这个数不小于2，true

```java
class Solution {
    public boolean hasGroupsSizeX(int[] deck) {
        int[] counts = new int[10000];
        for (int card : deck) {
            counts[card]++;
        }
        int gcd = counts[deck[0]];
        for (int count : counts) {
            if (count != 0) {
                gcd = getGCD(gcd, count);
                if (gcd < 2) return false;
            }
        }
        return true;
    }

    private int getGCD(int a, int b) {
        return a % b == 0 ? b : getGCD(b, a % b);
    }
}
```

