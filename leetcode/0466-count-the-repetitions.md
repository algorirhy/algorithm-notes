# [统计重复个数](https://leetcode-cn.com/problems/count-the-repetitions/)

暴力法

```java
class Solution {
    public int getMaxRepetitions(String s1, int n1, String s2, int n2) {
        char[] ch1 = s1.toCharArray();
        char[] ch2 = s2.toCharArray();
        int index = 0, num2 = 0;
        for (int num1 = 0; num1 < n1; num1++) {
            for (int i = 0; i < ch1.length; i++) {
                if (ch1[i] == ch2[index]) {
                    if (index == ch2.length - 1) {
                        index = 0;
                        num2++;
                    } else {
                        index++;
                    }
                }
            }
        }
        return num2 / n2;
    }
}
```

