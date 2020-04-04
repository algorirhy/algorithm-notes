# [验证IP地址](https://leetcode-cn.com/problems/validate-ip-address/)

```java
class Solution {
    public String validIPAddress(String IP) {
        if (IP.startsWith(":") || IP.startsWith(".") || IP.endsWith(":") || IP.endsWith(".")) {
            return "Neither";
        }
        String[] ip = IP.split("\\.|:");
        if(ip.length == 4) {
            return parseIPV4(ip);
        } else if (ip.length == 8) {
            return parseIPV6(ip);
        }
        return "Neither";
    }

    private String parseIPV4(String[] ip) {
        for (int i = 0; i < 4; i++) {
            if (ip[i].length() > 1 && ip[i].startsWith("0")) return "Neither";
            if (ip[i].startsWith("-")) return "Neither";
            int num = -1;
            try {
                num = Integer.parseInt(ip[i]);
            } catch (NumberFormatException e) {
                return "Neither";
            } 
            if (num > 255) return "Neither";
        }
        return "IPv4";
    }

    private String parseIPV6(String[] ip) {
        for (int i = 0; i < 8; i++) {
            int len = ip[i].length();
            if (len == 0 || len > 4) return "Neither";
            for (int j = 0; j < len; j++) {
                char c = ip[i].charAt(j);
                if ((c >= '0' && c <= '9') || (c >= 'a' && c <= 'f') || (c >= 'A' && c <= 'F')) {
                    continue;
                }
                return "Neither";
            }            
        }
        return "IPv6";
    }
}
```

