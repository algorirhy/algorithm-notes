# [航班预订统计](https://leetcode-cn.com/problems/corporate-flight-bookings/)

差分 + 前缀和

```c++
class Solution {
public:
    vector<int> corpFlightBookings(vector<vector<int>>& bookings, int n) {
        vector<int> res(n);
        for(auto &booking : bookings) {
            res[booking[0]-1] += booking[2];
            if (booking[1] < n) {
                res[booking[1]] -= booking[2];
            } 
        }
        for(auto i = 1; i < n; ++i) {
            res[i] += res[i-1];
        }
        return res;
    }
};
```

