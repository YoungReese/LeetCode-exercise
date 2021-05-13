https://leetcode.com/problems/ones-and-zeroes/

```c++
// 二维背包，一般 dp 需要三维，这里借鉴 01 背包的空间压缩方法，
// 将三维压缩到二维，因此需要逆向遍历
class Solution {
public:
    int findMaxForm(vector<string>& strs, int m, int n) {
        vector<vector<int>> dp(m + 1, vector<int>(n + 1, 0));
        for (string& s : strs) {
            auto [count0, count1] = countOneAndZero(s);
            for (int i = m; i >= count0; --i) {
                for (int j = n; j >= count1; --j) {
                    dp[i][j] = max(dp[i][j], dp[i - count0][j - count1] + 1);
                }
            }
        }
        return dp[m][n];
    }
private:
    pair<int, int> countOneAndZero(string s) {
        int count0 = 0, count1 = 0;
        for (int i = 0, n = s.size(); i < n; ++i) {
            if (s[i] == '0') count0++;
            else count1++;
        }
        return make_pair(count0, count1);
    }
};
```

