https://leetcode.com/problems/powx-n/

```c++
// O(log n)
class Solution {
public:
    double myPow(double x, int n) {
        bool flag = (n < 0) ? true : false;
        double y = powHelper(x, abs(n));
        return flag ? (1.0 / y) : y;
    }
private:
    double powHelper(const double& x, int n) {
        if (n == 0) return 1.0;
        if (n & 1) {
            double y = powHelper(x, n / 2);
            return y * y * x;
        } else {
            double y = powHelper(x, n / 2);
            return y * y;
        }
    }
};
```

