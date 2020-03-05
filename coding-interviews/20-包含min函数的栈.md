# [包含min函数的栈](https://www.nowcoder.com/practice/4c776177d2c04c2494f2555c9fcc1e49?tpId=13&tqId=11173&tPage=1&rp=1&ru=%2Fta%2Fcoding-interviews&qru=%2Fta%2Fcoding-interviews%2Fquestion-ranking)

### C++

```c++
class Solution {
public:
    void push(int value) {
        dataStack.push(value);
        if(minStack.empty()){
            minStack.push(value);
        }else if(value <= minStack.top()){
            minStack.push(value);
        }
    }
    void pop() {
        if(dataStack.top() == minStack.top()){
            minStack.pop();
        }
        dataStack.pop();
    }
    int top() {
        return dataStack.top();
    }
    int min() {
        return minStack.top();
    }

private:
    stack<int> dataStack, minStack;
};
```

#### Java

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

