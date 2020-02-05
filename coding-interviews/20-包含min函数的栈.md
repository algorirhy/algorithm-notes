# [包含min函数的栈](https://www.nowcoder.com/practice/4c776177d2c04c2494f2555c9fcc1e49?tpId=13&tqId=11173&tPage=1&rp=1&ru=%2Fta%2Fcoding-interviews&qru=%2Fta%2Fcoding-interviews%2Fquestion-ranking)

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
        if(dataStack,top() == minStack.top()){
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

