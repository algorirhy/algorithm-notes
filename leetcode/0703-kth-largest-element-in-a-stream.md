# [数据流中的第K大元素](https://leetcode-cn.com/problems/kth-largest-element-in-a-stream/)

```java
class KthLargest {
    private PriorityQueue<Integer> pq;
    private int k;

    public KthLargest(int k, int[] nums) {
        this.k = k;
        pq = new PriorityQueue<>();
        for (int num : nums) {
            add(num);
        }
    }
    
    public int add(int val) {
        if (pq.size() < k) {
            pq.add(val);
        } else if (val > pq.peek()) {
            pq.remove();
            pq.add(val);
        }
        return pq.peek();
    }
}
```

