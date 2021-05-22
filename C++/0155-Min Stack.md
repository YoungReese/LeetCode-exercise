https://leetcode.com/problems/min-stack/

```c++
// Methods pop, top and getMin operations will always be called on non-empty stacks.
class MinStack {
public:
    /** initialize your data structure here. */
    MinStack() {}
    
    void push(int val) {
        stk.push(val);
        int minVal = minStk.size() > 0 ? min(val, minStk.top()) : val;
        // int minVal = min(val, minStk.size() > 0 ? minStk.top() : val);
        minStk.push(minVal);
    }
    
    void pop() {
        stk.pop();
        minStk.pop();
    }
    
    int top() {
        return stk.top();
    }
    
    int getMin() {
        return minStk.top();
    }
private:
    stack<int> stk, minStk;
};

/**
 * Your MinStack object will be instantiated and called as such:
 * MinStack* obj = new MinStack();
 * obj->push(val);
 * obj->pop();
 * int param_3 = obj->top();
 * int param_4 = obj->getMin();
 */
```

