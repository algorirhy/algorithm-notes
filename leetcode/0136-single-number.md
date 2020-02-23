# [只出现一次的数字](https://leetcode-cn.com/problems/single-number/)

与两个相同的数进行异或运算，值不变。

```c++
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        int res = nums[0];
        for(int i = 1; i < nums.size(); i++){
            res ^= nums[i];
        }
        return res;
    }
};
```

