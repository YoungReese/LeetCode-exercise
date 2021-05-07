https://leetcode.com/problems/perfect-squares/

```c++
// dp[i] 表示数字 i 最少可以由几个完全平方数相加构成
class Solution {
public:
    int numSquares(int n) {
        vector<int> dp(n + 1, INT_MAX - 1);
        dp[0] = 0;
        for (int i = 1; i <= n; ++i) {
            for (int j = 1; j * j <= i; ++j) {
                dp[i] = min(dp[i], dp[i - j * j] + 1);
            }
        }
        return dp[n];
    }
};
```

>   **注意：还可以使用拉格朗日四平方和定理来解答，具体代码如下，知道有这个定理即可，正常解答还是使用上面的代码**
>
>   [0279.Perfect Squares](https://www.cnblogs.com/grandyang/p/4800552.html)
>
>   [拉格朗日四平方和定理说明](https://blog.csdn.net/l_mark/article/details/89044137)
>
>   [拉格朗日四平方和定理证明](https://zhuanlan.zhihu.com/p/104030654)

```c++
// 拉格朗日四平方和定理
// O(logn) 0ms
class Solution {
public:
    int numSquares(int n) {
        while(n % 4 == 0) n /= 4;
        if(n % 8 == 7) return 4;
        for(int i = 0; i * i <= n; ++i){
            int j = sqrt(n - i * i);
            if(i * i + j * j == n) 
                return !!i + !!j;
        }
        return 3;
    }
};
```

