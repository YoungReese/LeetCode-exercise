https://leetcode.com/problems/sqrtx/

```c++
class Solution {
public:
    int mySqrt(int x) { // 二分法
        if (x == 0 || x == 1) return x;
        int l = 1, r = x, mid, temp;
        while (l <= r) {
            mid = l + (r - l) / 2;
            temp = x / mid;
            if (mid == temp) return mid;
            if (mid < temp) l = mid + 1;
            else r = mid - 1;
        }
        return r;
    }
};
```



```c++
// 牛顿法公式： Xn+1 = (Xn + x / Xn) / 2 
// 推倒思路：Xn 位置建立切线方程交 x 轴位置 Xn+1
class Solution {
public:
    int mySqrt(int x) { // 牛顿法
        if (x == 0 || x == 1) return x;
        long long t = x;
        while (t * t > x) {
            t = (t + x / t) / 2;
        }
        return t;
    }
};
```

