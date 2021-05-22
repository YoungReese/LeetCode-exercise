https://leetcode.com/problems/implement-queue-using-stacks/

```c++
// All the calls to pop and peek are valid.
class MyQueue {
public:
    /** Initialize your data structure here. */
    MyQueue() {}
    
    /** Push element x to the back of queue. */
    void push(int x) {
        stk1.push(x);
    }
    
    /** Removes the element from in front of queue and returns that element. */
    int pop() {
        int res = peek();
        stk2.pop();
        return res;
    }
    
    /** Get the front element. */
    int peek() {
        if (stk2.size() == 0) {
            while (stk1.size() > 0) {
                stk2.push(stk1.top());
                stk1.pop();
            }
        }
        int res = stk2.top();
        return res;
    }
    
    /** Returns whether the queue is empty. */
    bool empty() {
        return !stk1.size() && !stk2.size();
    }  
private:
    stack<int> stk1, stk2;
};

/**
 * Your MyQueue object will be instantiated and called as such:
 * MyQueue* obj = new MyQueue();
 * obj->push(x);
 * int param_2 = obj->pop();
 * int param_3 = obj->peek();
 * bool param_4 = obj->empty();
 */
```

