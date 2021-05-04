https://leetcode.com/problems/factorial-trailing-zeroes/

```c++
// 统计因子 5 的个数，注意：25 = 5 * 5，因此有两个因子 5
class Solution {
public:
    int trailingZeroes(int n) {
        int res = 0;
        while (n) res += (n = n / 5);
        return res;
    }
};
```



```c++
class Solution {
public:
    int trailingZeroes(int n) {
        return n == 0 ? 0 : n / 5 + trailingZeroes(n / 5);
    }
};
```

