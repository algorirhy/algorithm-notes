# [用栈实现队列](https://leetcode-cn.com/problems/implement-queue-using-stacks/)

```java
class MyQueue {
    private Deque<Integer> pushStack, popStack;

    public MyQueue() {
        pushStack = new ArrayDeque<>();
        popStack = new ArrayDeque<>();
    }
    
    public void push(int x) {
        pushStack.push(x);
    }
    
    public int pop() {
        shift();
        return popStack.pop();
    }
    
    public int peek() {
        shift();
        return popStack.peek();
    }
    
    public boolean empty() {
        return pushStack.isEmpty() && popStack.isEmpty();
    }

    private void shift() {
        if (popStack.isEmpty()) {
            while (!pushStack.isEmpty()) {
                popStack.push(pushStack.pop());
            }
        }
    }
}
```

