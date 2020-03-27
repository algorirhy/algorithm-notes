# [数组中的第K个最大元素](https://leetcode-cn.com/problems/kth-largest-element-in-an-array/)

### 方法一

利用小顶堆

```java
class Solution {
    public int findKthLargest(int[] nums, int k) {
        PriorityQueue<Integer> pq = new PriorityQueue<>();
        for (int num : nums) {
            if (pq.size() < k) {
                pq.add(num);
            } else if (num > pq.peek()) {
                pq.remove();
                pq.add(num);
            }
        }
        return pq.peek();
    }
}
```



### 方法二

快速排序

```java
class Solution {
    public int findKthLargest(int[] nums, int k) {
        // 第k大等价于第n-k+1小,即快排确定的第n-k+1个元素
        return find(nums, 0, nums.length - 1, nums.length - k);
    }

    private int find(int[] nums, int left, int right, int k) {
        int pos = partition(nums, left, right);
        if (pos == k) {
            return nums[pos];
        } else if (pos < k) {
            return find(nums, pos + 1, right, k);
        } else {
            return find(nums, left, pos - 1, k);
        }
    }

    private int partition(int[] nums, int left, int right) {
        int pivot = nums[left];
        while (left < right) {
            while (left < right && nums[right] > pivot) right--;
            nums[left] = nums[right];
            while (left < right && nums[left] <= pivot) left++;
            nums[right] = nums[left];
        }
        nums[left] = pivot;
        return left;
    }
}
```

