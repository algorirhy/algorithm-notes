# [整数转罗马数字](https://leetcode-cn.com/problems/integer-to-roman/)

贪心算法

```java
class Solution {
    public String intToRoman(int num) {
        int[] values = {1000, 900, 500, 400, 100, 90, 50, 40, 10, 9, 5, 4, 1};
        String[] romans = 
            {"M", "CM", "D", "CD", "C", "XC", "L", "XL", "X", "IX", "V", "IV","I"};
        StringBuilder sb = new StringBuilder();
        for(int i = 0; i < 13; i++) {
            while (num >= values[i]) {
                sb.append(romans[i]);
                num -= values[i];
            }
        }
        return sb.toString();
    }
}
```

