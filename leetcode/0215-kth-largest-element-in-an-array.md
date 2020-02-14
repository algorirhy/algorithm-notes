# [数组中的第K个最大元素](https://leetcode-cn.com/problems/kth-largest-element-in-an-array/)

### 方法一

利用小顶堆

```c++
class Solution {
public:
    int findKthLargest(vector<int>& nums, int k) {
        if(k < 0 || k > nums.size()){
            return 0;
        }
        //小顶堆
        priority_queue<int, vector<int>, greater<int>> q;
        for(int i = 0; i < nums.size(); i++){
            if(q.size() < k){
                q.push(nums[i]);
            }else if (q.top() < nums[i]){
                q.pop();
                q.push(nums[i]);
            }
        }
        return q.top();        
    }
};
```



### 方法二

快速排序 + 二分查找

```c++
class Solution {
public:
    int findKthLargest(vector<int>& nums, int k) {
        if(k < 1 || k > nums.size()){
            return 0;
        }
        srand(time(nullptr)); 
        //第k大等价于第n-k+1小,即快排确定的第n-k+1个元素
        return findKthLargest(nums, 0, nums.size() - 1, nums.size() - k);
    }

private:
    int findKthLargest(vector<int>& nums, int l, int r, int s){
        if(l == r){
            return nums[l];
        }
        int p = partition(nums, l, r);
        if(p == s){
            return nums[p];
        }else if(p > s){
            return findKthLargest(nums, l, p - 1, s);
        }else{
            return findKthLargest(nums, p + 1, r, s);
        }
    }

    int partition(vector<int>& nums, int l, int r){
        int p = rand()%(r - l + 1) + l;
        swap(nums[l], nums[p]);
        
        int j = l;
        for (int i = l + 1; i <= r; i++) {
            if (nums[i] < nums[l]) {
                swap(nums[i], nums[j + 1]);
                j++;
            }
        }
        swap(nums[l], nums[j]);
        return j;
    }
}; 
```

或者

```c++
class Solution {
public:
    int findKthLargest(vector<int>& nums, int k) {
        if(k < 1 || k > nums.size()){
            return 0;
        }
        srand(time(nullptr)); 
        //第k大等价于第n-k+1小,即快排确定的第n-k+1个元素
        return findKthLargest(nums, 0, nums.size() - 1, nums.size() - k);
    }

private:
    int findKthLargest(vector<int>& nums, int l, int r, int s){
        if(l == r){
            return nums[l];
        }
        int p = partition(nums, l, r);
        if(p == s){
            return nums[p];
        }else if(p > s){
            return findKthLargest(nums, l, p - 1, s);
        }else{
            return findKthLargest(nums, p + 1, r, s);
        }
    }

	int partition(vector<int>& nums, int l, int r){
        int p = rand()%(r - l + 1) + l;
        swap(nums[l], nums[p]);
        
        int temp = nums[l];
        while(l < r){
            while(l < r && nums[r] > temp) r--;
            nums[l] = nums[r];
            while(l < r && nums[l] <= temp) l++;
            nums[r] = nums[l];
        }
        nums[l] = temp;
        return l;
    }
};
```

