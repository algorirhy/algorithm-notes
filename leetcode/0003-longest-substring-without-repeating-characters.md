# [无重复字符的最长子串](https://leetcode-cn.com/problems/longest-substring-without-repeating-characters/)

滑动窗口

```C++
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        if(!s.size())
            return 0;
        unordered_set<char> us;
        int res = 0, left = 0;
        for(int i = 0; i < s.size(); i++){
            while(us.find(s[i]) != us.end()){
                us.erase(s[left]);
                left++;
            }
            res = max(res, i+1-left);
            us.insert(s[i]);
        }
        return res;
    }
};
```
