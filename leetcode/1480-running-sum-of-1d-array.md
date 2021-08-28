# [一维数组的动态和](https://leetcode-cn.com/problems/running-sum-of-1d-array)

```c++
class Solution {
public:
    vector<int> runningSum(vector<int>& nums) {
         int n = nums.size();
         for (int i = 1; i < n; i++) {
             nums[i] += nums[i-1];
         }
         return nums;
    }
};
```
