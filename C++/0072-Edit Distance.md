https://leetcode.com/problems/edit-distance/

```c++
// O(mn) O(mn)
class Solution {
public:
    int minDistance(string word1, string word2) {
        int m = word1.size(), n = word2.size();
        vector<vector<int>> dp(m + 1, vector<int>(n + 1, 0));
        for (int i = 0; i <= m; i++) dp[i][0] = i;
        for (int j = 0; j <= n; j++) dp[0][j] = j;
        
        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                if (word1[i - 1] == word2[j - 1]) {
                    dp[i][j] = dp[i - 1][j - 1];
                } else { // word1:  delete           insert          replace
                    dp[i][j] = min(dp[i - 1][j], min(dp[i][j - 1], dp[i - 1][j - 1])) + 1;
                }
            }
        }
        
        return dp[m][n];
    }
};
```



```c++
// O(mn) O(min(m, n))
class Solution {
public:
    int minDistance(string word1, string word2) {
        if (word1.size() < word2.size()) swap(word1, word2);
        
        int m = word1.size(), n = word2.size();
        vector<int> dp(n + 1, 0);
        for (int j = 0; j <= n; j++) dp[j] = j;
        
        for (int i = 1; i <= m; i++) {
            int pre = dp[0];
            dp[0] = i;
            for (int j = 1; j <= n; j++) {
                int tmp = dp[j];
                if (word1[i - 1] == word2[j - 1]) {
                    dp[j] = pre;
                } else {    // delete     insert     replace   <=  word1
                    dp[j] = min(dp[j], min(dp[j - 1], pre)) + 1;
                }
                pre = tmp;
            }
        }
        
        return dp[n];
    }
};
```

