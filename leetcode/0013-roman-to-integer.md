# [罗马数字转整数](https://leetcode-cn.com/problems/roman-to-integer)

```java
class Solution {
    public int romanToInt(String s) {
        if (s.length() == 0) return 0;
        int res = 0;
        int preNum = getNum(s.charAt(0));
        for (int i = 1; i < s.length(); i++) {
            int num = getNum(s.charAt(i));
            if (preNum < num) {
                res -= preNum;
            } else {
                res += preNum;
            }
            preNum = num;
        }
        res += preNum;
        return res;
    }

    private int getNum(char ch) {
        switch (ch) {
            case 'I' : return 1;
            case 'V' : return 5;
            case 'X' : return 10;
            case 'L' : return 50;
            case 'C' : return 100;
            case 'D' : return 500;
            case 'M' : return 1000;
            default : return 0;
        }
    }
}
```

