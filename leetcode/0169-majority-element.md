# [多数元素](https://leetcode-cn.com/problems/majority-element/)

### 方法一

哈希表

```java
class Solution {
    public int majorityElement(int[] nums) {
        Map<Integer, Integer> map = new HashMap<>();
        int majorityCount = nums.length / 2;
        for (int num : nums) {
            int count = map.getOrDefault(num, 0) + 1;
            if (count > majorityCount) {
                return num;
            }
            map.put(num, count);
        }
        return 0;
    }
}
```

### 方法二

摩尔投票

```java
class Solution {
    public int majorityElement(int[] nums) {
        int candidate = nums[0], count = 0;
        for (int num : nums) {
            if (count == 0) {
                candidate = num;
                count++;
            } else if (candidate == num) {
                count++;
            } else {
                count--;
            }
        }
        return candidate;
    }
}
```

