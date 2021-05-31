https://leetcode.com/problems/palindromic-substrings/

```c++
// 中心扩展，对于每一个位置，可以是奇数中心，也可以是偶数中心
class Solution {
public:
    int countSubstrings(string s) {
        int res = 0;
        for (int i = 0, n = s.size(); i < n; ++i) {
            res += extendSubstrings(i, i, s, n);     // 奇数长度
            res += extendSubstrings(i, i + 1, s, n); // 偶数长度
        }
        return res;
    }
private:
    int extendSubstrings(int left, int right, const string& s, const int& n) {
        int count = 0;
        while (left >= 0 && right < n && s[left--] == s[right++]) ++count;
        return count;
    }
};
```



```c++
// dp[i][j] = true => s[i...j] 是个回文串
class Solution {
public:
    int countSubstrings(string s) {
        int n = s.size();
        vector<vector<bool>> dp(n, vector<bool>(n, false));
        int res = 0;
        for (int j = 0; j < n; ++j) {  // 对于每一个位置 j ，这里一定要从 j 往前看，因为需要用到之前的状态
            dp[j][j] = true;
            ++res;
            for (int i = j - 1; i >= 0; --i) { // 尝试位置 j 之前的每一个位置 i
                if (s[i] == s[j]) {            // i 和 j 位置字符串如果相等
                    if (i + 1 == j || dp[i + 1][j - 1]) { // i 和 j 相邻或者 (i..j) 之间部分是回文
                        dp[i][j] = true;       // 此时 [i...j] 构成回文
                        ++res;
                    }
                }
            }
        }
        return res;
    }
};
```

