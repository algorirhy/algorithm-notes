# [用队列实现栈](https://leetcode-cn.com/problems/implement-stack-using-queues)

一个队列实现，入栈时间复杂度为O(n)，出栈时间复杂度为O(1)。

```c++
class MyStack {
private:
    queue<int> q;

public:
    /** Initialize your data structure here. */
    MyStack() {
        
    }
    
    /** Push element x onto stack. */
    void push(int x) {
        int size = q.size();
        q.push(x);
        for(int i = 0; i < size; i++){
            int tmp = q.front();
            q.pop();
            q.push(tmp);
        }
    }
    
    /** Removes the element on top of the stack and returns that element. */
    int pop() {
        int tmp = q.front();
        q.pop();
        return tmp;
    }
    
    /** Get the top element. */
    int top() {
        return q.front();
    }
    
    /** Returns whether the stack is empty. */
    bool empty() {
        return q.empty();
    }
};
```

