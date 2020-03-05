# [最小栈](https://leetcode-cn.com/problems/min-stack/)

```java
class MinStack {

    private LinkedList<Integer> dataStack, minStack;

    public MinStack() {
        dataStack = new LinkedList<>();
        minStack = new LinkedList<>();
    }
    
    public void push(int x) {
        dataStack.addFirst(x);
        if (minStack.isEmpty() || minStack.peekFirst() >= x) {
            minStack.addFirst(x);
        } 
    }
    
    public void pop() {
        //使用 == 报错
        if(dataStack.peekFirst().equals(minStack.peekFirst())){
            minStack.removeFirst();
        }
        dataStack.removeFirst();
    }
    
    public int top() {
        return dataStack.peekFirst();
    }
    
    public int getMin() {
        return minStack.peekFirst();
    }
}
```

