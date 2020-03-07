# [队列的最大值](https://leetcode-cn.com/problems/dui-lie-de-zui-da-zhi-lcof/)

维护两个队列，一个正常入队出队，一个递减队列。

```java
class MaxQueue {

    ArrayDeque<Integer> queue;
    ArrayDeque<Integer> maxQueue;

    public MaxQueue() {
        queue = new ArrayDeque();
        maxQueue = new ArrayDeque();
    }
    
    public int max_value() {
        if (maxQueue.isEmpty()) {
            return -1;
        }  
        return maxQueue.peekFirst();
    }
    
    public void push_back(int value) {
        queue.offer(value);
        while (!maxQueue.isEmpty() && value > maxQueue.peekLast()) {
            maxQueue.pollLast();
        }
        maxQueue.offerLast(value);
    }
    
    public int pop_front() {
        if (queue.isEmpty()) {
            return -1;
        }
        int res = queue.poll();
        if (res == maxQueue.peekFirst()) {
            maxQueue.pollFirst();
        }
        return res;
    }
}
```

