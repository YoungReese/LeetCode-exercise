https://leetcode.com/problems/daily-temperatures/

```c++
// 维持一个单调递减的栈，比较的事温度值，存储的是角标
class Solution {
public:
    vector<int> dailyTemperatures(vector<int>& T) {
        int n = T.size();
        vector<int> res(n, 0);
        stack<int> stk;
        for (int i = 0; i < n; ++i) {
            while (!stk.empty() && T[i] > T[stk.top()]) {
                int preIndex = stk.top(); stk.pop();
                res[preIndex] = i - preIndex;
            }
            stk.push(i);
        }
        return res;
    }
};
```

