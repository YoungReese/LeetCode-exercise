https://leetcode.com/problems/decode-ways/

```c++
// dp[i]：表示字符串s[0...i)有多少种编码方式
class Solution {
public:
    int numDecodings(string s) {
        int n = s.size();
        if (n >= 1 && s[0] == '0') return 0;
        
        vector<int> dp(n + 1, 1);
        int pre = s[0] - '0';
        for (int i = 2; i <= n; ++i) {
            int cur = s[i - 1] - '0';
            if ((pre == 0 || pre > 2) && cur == 0) return 0; //  only 10 and 20 is ok
            if ((pre > 0 && pre < 2) || (pre == 2 && cur <= 6)) {
                if (cur != 0) dp[i] = dp[i - 1] + dp[i - 2];
                else dp[i] = dp[i - 2];
            } else dp[i] = dp[i - 1];
            pre = cur;
        }
        
        return dp[n];
    }
};
```

