https://leetcode.com/problems/2-keys-keyboard/

```c++
// dp[i]：表示延展到长度 i 的最少操作次数
// 对于每个位置 j，如果 j 可以被 i 整除，那么长度 i 就可以由长度 j 操作得到，
// 其操作次数等价于把一个长度为 1 的 A 延展到长度为 i / j 个 A
// O(n logn)  O(n)
class Solution {
public:
    int minSteps(int n) {
        vector<int> dp(n + 1);
        for (int i = 2, h = sqrt(n); i <= n; ++i) {
            dp[i] = i; // 最多的步骤
            for (int j = 2; j <= h; ++j) {
                if (i % j == 0) {
                    dp[i] = dp[j] + dp[i / j];
                    break;
                } 
            }
        }
        return dp[n];
    }
};
```



```c++
// math
// O(sqrt(n))  O(1)
// 当 n >= 2 的时候，最优策略就是尽可能地生成 n 的最大因数（n / d）个 A，然后进行 Copy 1 次 Paste (d - 1) 次操作，
// 为使 (n / d) 尽可能的大，只能使 d 尽可能的小，于是 d 从 2 开始循环。
// 当找到一个 d 之后，我们接下来只需要解决生成 (n / d) 个 A 的问题，所以在循环中让 n 变为 (n / d) 即可。
class Solution {
public:
    int minSteps(int n) {
        int res = 0, d = 2;
        while (n > 1) {
            while (n % d == 0) {
                res += d;
                n /= d;
            }
            d++;
        }
        return res;
    }
};
```

