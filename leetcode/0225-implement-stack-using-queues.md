# [用队列实现栈](https://leetcode-cn.com/problems/implement-stack-using-queues)

```java
class MyStack {
    Deque<Integer> q;

    public MyStack() {
        q = new ArrayDeque<>();
    }
    
    public void push(int x) {
        int size = q.size();
        q.add(x);
        // 把之前的元素都出队再入队，保证后进先出
        for (int i = 0; i < size; i++) {
            q.add(q.remove());
        }
    }
    
    public int pop() {
        return q.remove();
    }

    public int top() {
        return q.peek();
    }

    public boolean empty() {
        return q.isEmpty();
    }
}
```

