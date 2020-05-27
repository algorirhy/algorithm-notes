# [和可被 K 整除的子数组](https://leetcode-cn.com/problems/subarray-sums-divisible-by-k)

```java
class Solution {
    public int subarraysDivByK(int[] A, int K) {
        Map<Integer, Integer> map = new HashMap<>();
        map.put(0, 1);
        int sum = 0, res = 0;
        for (int num : A) {
            sum += num;
            // 注意 Java 取模的特殊性，当被除数为负数时取模结果为负数，需要纠正
            int mod = (sum % K + K) % K;
            int same = map.getOrDefault(mod, 0);
            res += same;
            map.put(mod, same + 1);
        }
        return res;
    }
}
```

