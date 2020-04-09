# [加油站](https://leetcode-cn.com/problems/gas-station/)

```java
class Solution {
    public int canCompleteCircuit(int[] gas, int[] cost) {
        // 遇到第一个无法到达的点 i，直接更换起始点为 i+1
        int total = 0, sum = 0, start = 0;
        for (int i = 0; i < gas.length; i++) {
            total += gas[i] - cost[i];
            sum += gas[i] - cost[i];
            if (sum < 0) {
                sum = 0;
                start = i + 1;
            }
        }
        return total < 0 ? -1 : start;
    }
}
```

