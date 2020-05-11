# [最小栈](https://leetcode-cn.com/problems/min-stack/)

```java
class MinStack {
    private Deque<Integer> dataStack, minStack;

    public MinStack() {
        dataStack = new ArrayDeque<>();
        minStack = new ArrayDeque<>();
    }
    
    public void push(int x) {
        dataStack.push(x);
        if (minStack.isEmpty() || minStack.peek() >= x) {
            minStack.push(x);
        } 
    }
    
    public void pop() {
        if(dataStack.peek().equals(minStack.peek())){
            minStack.pop();
        }
        dataStack.pop();
    }
    
    public int top() {
        return dataStack.peek();
    }
    
    public int getMin() {
        return minStack.peek();
    }
}
```

