# [复原IP地址](https://leetcode-cn.com/problems/restore-ip-addresses/)

今天招银网络笔试考了一个类似的，可惜没做出来，看样子还是题刷少了。

### 方法一

暴力法，简直就是暴力美学。

```java
class Solution {
    public List<String> restoreIpAddresses(String s) {
        List<String>  res = new ArrayList<>();
        StringBuilder ip = new StringBuilder();

        for (int a = 1; a < 4; a++) {
            for (int b = 1; b < 4; b++) {
                for (int c = 1; c < 4; c++) {
                    for (int d = 1; d < 4; d++) {
                        if (a + b + c + d == s.length()) {
                            int n1 = Integer.parseInt(s.substring(0, a));
                            int n2 = Integer.parseInt(s.substring(a, a + b));
                            int n3 = Integer.parseInt(s.substring(a + b, a + b + c));
                            int n4 = Integer.parseInt(s.substring(a + b + c));

                            if (n1 <= 255 && n2 <= 255 && n3 <= 255 && n4 <= 255) {
                                ip.append(n1).append('.').append(n2)
                                    .append('.').append(n3).append('.').append(n4);
                                //长度不变 防止 1 1 1 010 -> 1.1.1.10
                                if (ip.length() == s.length() + 3)
                                    res.add(ip.toString());
                                ip.delete(0, ip.length());
                            }
                        }
                    }
                }
            }
        }
        return res;
    }
}
```

### 方法二

回溯

```java
class Solution {
    public List<String> restoreIpAddresses(String s) {
        List<String> res = new ArrayList<>();
        backtrack(0, "", 4, s, res);
        return res;
    }

    private void backtrack(int pos, String ip, int step, String s, List<String> res) {
        if (pos == s.length() && step == 0) {
            //去掉最后一个小数点
            res.add(ip.substring(0, ip.length() - 1));
            return;
        }
        if (step < 0) return;
        for (int j = pos; j < pos + 3; j++) {
            if (j < s.length()) {
                //0开头，单独作为一部分
                if (j == pos && s.charAt(j) == '0') {
                    backtrack(j+1, ip + "0.", step-1, s, res);
                    break;
                }
                if (Integer.parseInt(s.substring(pos, j + 1)) <= 255) {
                    backtrack(j+1, ip + s.substring(pos, j+1) + '.', step-1, s, res);
                }
            }
        }
    }
}
```

