https://leetcode.com/problems/valid-parentheses/

```c++
// Given a string s containing just the characters '(', ')', '{', '}', '[' and ']'
class Solution {
public:
    bool isValid(string s) {
        stack<char> stk;
        for (char& c : s) {
            if (c == '(' || c == '{' || c == '[') stk.push(c);
            else if ((stk.size() == 0)
                     || (c == ')' && stk.top() != '(') 
                     || (c == '}' && stk.top() != '{')
                     || (c == ']' && stk.top() != '[')) return false;
            else stk.pop();
        }
        return stk.size() == 0;
    }
};
```

