# [两数之和](https://leetcode.com/problems/two-sum/)

### 方法一

暴力法

```C++
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        for(int i=0; i<nums.size(); i++){
            for(int j=i+1; j<nums.size(); j++){
                if(nums[j]==target-nums[i]){
                    return {i,j};
                }
            }
        }
        return {-1,-1};
    }
};
```

### 方法二

利用map

```C++
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
    map<int, int> mp;
    vector<int> ans;
    int len = (int) nums.size();
    for (int i = 0; i < len; i++) {
        if (mp.find(target - nums[i]) != mp.end()) {
            ans.push_back(mp[target - nums[i]]);
            ans.push_back(i);
            return ans;
        }
        mp[nums[i]] = i;
    }
    	return ans;
    }
};
```

