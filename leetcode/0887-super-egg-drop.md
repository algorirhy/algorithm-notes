# [鸡蛋掉落](https://leetcode-cn.com/problems/super-egg-drop/)

动态规划 + 二分搜索

```java
class Solution {
    Map<Integer, Integer> map = new HashMap<>();

    public int superEggDrop(int K, int N) {
        return dp(K, N);
    }

    private int dp(int K, int N) {
        if (!map.containsKey(N * 100 + K)) {
            int res;
            if (N == 0) {
                res = 0;
            } 
            else if (K == 1) {
                res = N;
            } else {
                int left = 1, right = N;
                while (left + 1 < right) {
                    int mid = (left + right) / 2;
                    int t1 = dp(K - 1, mid - 1);
                    int t2 = dp(K, N - mid);
                    if (t1 < t2) {
                        left = mid;
                    } else if (t1 > t2) {
                        right = mid;
                    } else {
                        left = right = mid;
                    }   
                }
                res = 1 + Math.min(Math.max(dp(K - 1, left - 1), dp(K, N - left)),
                                   Math.max(dp(K - 1, right - 1), dp(K, N - right)));
            }
            map.put(N * 100 + K, res);
        }
        return map.get(N * 100 + K);
    }
}
```

