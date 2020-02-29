# [接雨水](https://leetcode-cn.com/problems/trapping-rain-water/)

### 方法一

暴力法

```c++
class Solution {
public:
    int trap(vector<int>& height) {
        int ans = 0;
        int size = height.size();
        if(size == 0)
            return ans;
        for(int i = 1; i < size - 1; i++){
            int left_max = 0, right_max = 0;
            for(int j = i; j >= 0; j--)
                left_max = max(left_max, height[j]);
            for(int j = i; j < size; j++)
                right_max = max(right_max, height[j]);
            ans += min(left_max, right_max) - height[i];
        }
        return ans;
    }
};
```



### 方法二

动态编程 打表

```c++
class Solution {
public:
    int trap(vector<int>& height) {
        int ans = 0;
        int size = height.size();
        if(size == 0)
            return ans;
        vector<int> left_max(size), right_max(size);

        left_max[0] = height[0];
        for(int i = 1; i < size; i++)
            left_max[i] = max(height[i], left_max[i-1]);

        right_max[size-1] = height[size-1];
        for(int i = size-2; i >= 0; i--)
            right_max[i] = max(height[i], right_max[i+1]);

        for(int i = 1; i < size - 1; i++)
            ans += min(left_max[i], right_max[i]) - height[i];
        return ans;
    }
};
```



### 方法三

利用栈

```c++
class Solution {
public:
    int trap(vector<int>& height) {
        int ans = 0, cur = 0;
        int size = height.size();
        if(size == 0)
            return ans;
        stack<int> stk;
        while(cur < size){
            while(!stk.empty() && height[cur] > height[stk.top()]){
                int top = stk.top();
                stk.pop();
                if(stk.empty())
                    break;
                int distance = cur - stk.top() - 1;
                int bound_height = min(height[cur], height[stk.top()]) - height[top];
                ans += distance * bound_height;
            }
            stk.push(cur++);
        }
        return ans;
    }
};
```



### 方法四

双指针

```C++
class Solution {
public:
    int trap(vector<int>& height) {
        int ans = 0;
        int size = height.size();
        if(size == 0)
            return ans;
        int left = 0, right = size - 1;
        int left_max = 0, right_max = 0;
        while(left < right){
            //左边相对较低
            if(height[left] < height[right]){
                //若大于等于左边最高，更新最高，否则计算高度差
                height[left] >= left_max ? (left_max = height[left]) : \
                    ans += left_max - height[left];
                left++;
            }else{
                height[right] >= right_max ? (right_max = height[right]) : \
                    ans += right_max - height[right];
                right--;
            }
        }
        return ans;
    }
};
```

