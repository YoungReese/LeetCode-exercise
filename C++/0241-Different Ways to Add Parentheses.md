https://leetcode.com/problems/different-ways-to-add-parentheses/

```c++
// O(n logn)
// 分治法 + 记忆化 => 按照 operator 进行分割
class Solution {
public:
    vector<int> diffWaysToCompute(string expression) {
        int n = expression.size();
        vector<vector<vector<int>>> memo(n, vector<vector<int>>(n, vector<int>()));
        return diffWays(expression, 0, n - 1, memo);
    }
private:
    vector<int> diffWays(const string& expression, int start, int end, 
                         vector<vector<vector<int>>>& memo) {
        
        if (start > end) return {};
        if (start == end) return { expression[start] - '0' };
        if (memo[start][end].size()) return memo[start][end];
        
        vector<int> res;
        for (int i = start; i <= end; ++i) {
            if (expression[i] == '+' || expression[i] == '-' || expression[i] == '*') {
                vector<int> leftRes = diffWays(expression, start, i - 1, memo);
                vector<int> rightRes = diffWays(expression, i + 1, end, memo);
                for (int& leftVal : leftRes) {
                    for (int& rightVal : rightRes) {
                        if (expression[i] == '+') res.push_back(leftVal + rightVal);
                        else if (expression[i] == '-') res.push_back(leftVal - rightVal);
                        else res.push_back(leftVal * rightVal);
                    }
                }
            }
        }
        
        if (res.empty()) res.push_back(stoi(expression.substr(start, end - start + 1)));
        memo[start][end] = res;
        
        return res;
    }
};
```



```c++
// not easy to understand
class Solution {
public:
    vector<int> diffWaysToCompute(string expression) {
        vector<int> nums;
        vector<char> opr;
        int num = 0;
        char op = ' ';
        istringstream is(expression + '+');  
        string s;
        while(is >> num && is >> op) {
            nums.push_back(num);
            opr.push_back(op);
        }
        
        int n = nums.size();
        vector<vector<vector<int>>> dp(n, vector<vector<int>>(n, vector<int>()));
        for (int i = 0; i < n; ++i) {
            for (int j = i; j >= 0; --j) {
                if (i == j) dp[j][i].push_back(nums[i]);
                else {
                    for (int k = j; k < i; ++k) {
                        for (int& left : dp[j][k]) {
                            for (int & right : dp[k + 1][i]) {
                                if (opr[k] == '+') dp[j][i].push_back(left + right);
                                else if (opr[k] == '-') dp[j][i].push_back(left - right);
                                else dp[j][i].push_back(left * right);
                            }
                        }
                    }
                }
            }
        }
        
        return dp[0][n - 1];
    }
};
```

