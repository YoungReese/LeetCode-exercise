https://leetcode.com/problems/regular-expression-matching/

```c++
// 建议使用这种写法
class Solution {
public:
    bool isMatch(string s, string p) {
        int m = s.size(), n = p.size();
        if (n == 0) return m == 0;
        vector<vector<bool>> dp(m + 1, vector<bool>(n + 1, false));
        dp[0][0] = true;
        for (int j = 2; j <= n; ++j) {
            if (p[j - 1] == '*') dp[0][j] = dp[0][j - 2];
        }
        for (int i = 1; i <= m; ++i) {
            for (int j = 1; j <= n; ++j) {
                if (p[j - 1] != '*') {
                    if (p[j - 1] == s[i - 1] || p[j - 1] == '.') {
                        dp[i][j] = dp[i - 1][j - 1];
                    }
                } else { // cp[j - 1] == '*'
                    if (p[j - 2] != s[i - 1] && p[j - 2] != '.') {
                        dp[i][j] = dp[i][j - 2];
                    } else {
                        dp[i][j] = dp[i - 1][j] || dp[i][j - 2];
                    }
                }
            }
        }
        return dp[m][n];
    }
};
```



```c++
// 解题重点是关注 p 中的 '*'
// 这种写法容易漏掉匹配单尝试 0 次使用的情况（见 21 行和 22 行）
class Solution {
public:
    bool isMatch(string s, string p) {
        int m = s.size(), n = p.size();
        if (n == 0) return m == 0;
        vector<vector<bool>> dp(m + 1, vector<bool>(n + 1, false));
        dp[0][0] = true;
        for (int j = 2; j <= n; ++j) {
            if (p[j - 1] == '*') dp[0][j] = dp[0][j - 2];
        }
        for (int i = 1; i <= m; ++i) {
            for (int j = 1; j <= n; ++j) {
                if (p[j - 1] != '*') {
                    if (p[j - 1] == s[i - 1] || p[j - 1] == '.') {
                        dp[i][j] = dp[i - 1][j - 1];
                    }
                } else { // cp[j - 1] == '*'
                    if (p[j - 2] == s[i - 1] || p[j - 2] == '.') { // i 位置可以匹配
                        // 使用 n（1 包括在 n 中） 次或者 0 次，利用前向推导累计
                        dp[i][j] = dp[i - 1][j] || dp[i][j - 2];
                    } else {
                        // 使用 0 次，因为 j 和 j - 1 位置不使用
                        dp[i][j] = dp[i][j - 2];
                    }
                }
            }
        }
        return dp[m][n];
    }
};
```



```java
// java 写法，和第一种 c++ 写法一致，这里做了一下详细解释
class Solution {
    public boolean isMatch(String s, String p) {
        int m = s.length(), n = p.length();
        if (n == 0) return m == 0;
        boolean[][] dp = new boolean[m + 1][n + 1];
        char[] cs = s.toCharArray();
        char[] cp = p.toCharArray();
        dp[0][0] = true;
        for (int j = 1; j <= n; ++j) {
            if (cp[j - 1] == '*') dp[0][j] = dp[0][j - 2]; // 使用 0 次的初始化操作
        }
        for (int i = 1; i <= m; ++i) {
            for (int j = 1; j <= n; ++j) {
                if (cp[j - 1] != '*') {
                    if (cp[j - 1] == '.' || cp[j - 1] == cs[i - 1]) {
                        dp[i][j] = dp[i - 1][j - 1];
                    }
                } else { // cp[j - 1] == '*'
                    if (cp[j - 2] != cs[i - 1] && cp[j - 2] != '.') {
                        dp[i][j] = dp[i][j - 2];
                    } else {
                        /**
                         * dp[i - 1][j] => 表示 j 除了匹配 i 位置，还将尝试匹配 i - 1 位置，即 ？* 使用 n 次
                         * dp[i][j - 1] => 表示 j - 1 位置匹配 i 位置，位置 j 不使用，即 ？* 使用 1 次
                         * dp[i][j - 1] => 表示 j - 2 位置匹配 i 位置，位置 j 和 j - 1 不使用，即 ？* 使用 0 次
                         */
                        //               n 次             1 次             0 次
                        // dp[i][j] = dp[i - 1][j] || dp[i][j - 1] || dp[i][j - 2];
                        dp[i][j] = dp[i - 1][j] || dp[i][j - 2]; // 1 次可以被包含在 n 次中
                    }
                }
            }
        }
        return dp[m][n];
    }
}
```

