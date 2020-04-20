# [子集](https://leetcode-cn.com/problems/subsets/)

### 方法一

回溯法

```java
class Solution {
    public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> res = new ArrayList<>();
        backTrack(nums, 0, res, new ArrayList<>());
        return res;
    }

    private void backTrack(int[] nums, int index, List res, List tmp) {
        res.add(new ArrayList(tmp));
        for (int i = index; i < nums.length; i++) {
            tmp.add(nums[i]);
            backTrack(nums, i + 1, res, tmp);
            tmp.remove(tmp.size() - 1);
        }
    }
}
```

### 方法二

二进制位

```java
class Solution {
    public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> res = new ArrayList<>();
        // 一共 2^n 种，每个数字代表一种，按位选取，例如：0 -> 000 -> []; 7 -> 111 -> [1,2,3]
        for (int i = 0; i < (1 << nums.length); i++) {
            List<Integer> list = new ArrayList<>();
            for (int j = 0; j < nums.length; j++) {
                if (((i >> j) & 1) == 1) {
                    list.add(nums[j]);
                }
            }
            res.add(list);
        }
        return res;
    }
}
```

