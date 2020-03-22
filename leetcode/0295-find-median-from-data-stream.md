# [数据流的中位数](https://leetcode-cn.com/problems/find-median-from-data-stream/)

```java
class MedianFinder {
    private int count;
    private PriorityQueue<Integer> maxHeap;
    private PriorityQueue<Integer> minHeap;

    public MedianFinder() {
        maxHeap = new PriorityQueue<>((x, y) -> (y - x));
        minHeap = new PriorityQueue<>();
    }
    
    public void addNum(int num) {
        count++;
        maxHeap.add(num);
        minHeap.add(maxHeap.remove());
        // 如果两个堆合起来的元素个数是奇数，小顶堆要拿出堆顶元素给大顶堆
        if ((count & 1) == 1) {
            maxHeap.add(minHeap.remove());
        }
    }
    
    public double findMedian() {
        if ((count & 1) == 0) {
            return (maxHeap.peek() + minHeap.peek()) / 2.0;
        }
        return (double)maxHeap.peek();
    }
}
```

