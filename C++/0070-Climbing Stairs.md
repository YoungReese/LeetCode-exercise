https://leetcode.com/problems/climbing-stairs/

```c++
class Solution {
public:
    int climbStairs(int n) {
        if (n == 1 || n == 2) return n;
        int n0 = 1, n1 = 1, n2;
        for (int i = 2; i <= n; ++i) {
            n2 = n0 + n1;
            n0 = n1;
            n1 = n2;
        }
        return n2;
    }
};
```


