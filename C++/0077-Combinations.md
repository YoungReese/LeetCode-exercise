https://leetcode.com/problems/combinations/

```c++
class Solution {
public:
    vector<vector<int>> combine(int n, int k) {
        vector<int> ans;
        vector<vector<int>> res;
        backtracking(n, k, 1, ans, res);
        return res;
    }
private:
    void backtracking(const int& n, const int& k, int start,
                      vector<int>& ans, vector<vector<int>>& res) {
        if (ans.size() == k) {
            res.push_back(ans);
            return;
        }
        
        for (int i = start; i <= n; ++i) {
            ans.push_back(i);
            backtracking(n, k, i + 1, ans, res);
            ans.pop_back();
        }
    }
};
```



```c++
class Solution {
public:
    vector<vector<int>> combine(int n, int k) {
        vector<int> ans;
        vector<vector<int>> res;
        backtracking(n, k, 1, ans, res);
        return res;
    }
private:
    void backtracking(int& n, int& k, int start, 
                      vector<int>& ans, 
                      vector<vector<int>>& res) {
        if (ans.size() == k) {
            res.push_back(ans);
            return;
        }
        // 还有 k - ans.size() 个空位，所以 [i...n] 中至少要有 k - ans.size() 个元素
        // i 这里占据一个位置，所以 i 最多为 n - (k - ans.size() - 1)
        for (int i = start; i <= n - (k - ans.size() - 1); ++i) {
            ans.push_back(i);
            backtracking(n, k, i + 1, ans, res);
            ans.pop_back();
        }
    }
};
```

