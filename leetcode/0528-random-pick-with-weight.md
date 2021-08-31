# [按权重随机选择](https://leetcode-cn.com/problems/random-pick-with-weight/)

彩票调度 步长调度

https://pages.cs.wisc.edu/~remzi/OSTEP/Chinese/09.pdf 

### 前缀和

```c++
class Solution {
public:
    int totalWeights = 0;
    vector<int> weights;

    Solution(vector<int>& w) {
        for (auto w_ : w) {
            weights.push_back(totalWeights);
            totalWeights += w_;
        }
    }
    
    int pickIndex() {
        int rnd = rand() % totalWeights;
        int i = 0;

        for (i=1; i < weights.size(); i++) {
            if (weights[i] > rnd) {
                break;
            }
        }

        return i-1;
    }
};
```



### 前缀和 + 二分查找

```c++
class Solution {
public:
    int totalWeights = 0;
    vector<int> weights;

    Solution(vector<int>& w) {
        for (auto w_ : w) {
            weights.push_back(totalWeights);
            totalWeights += w_;
        }
    }
    
    int pickIndex() {
        int rnd = rand() % totalWeights;
        int left = 0;
        int right = weights.size() - 1;

        while (left < right) {
            int mid =left + (right - left) / 2;
            if (weights[mid] > rnd) {
                right = mid;
            } else {
                left = mid + 1;
            }
        }
        return left;
    }
};
```

