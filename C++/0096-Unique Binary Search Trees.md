https://leetcode.com/problems/unique-binary-search-trees/

```c++
class Solution {
public:
    int numTrees(int n) {
        if (n == 1) return 1;
        vector<vector<int>> memo(n, vector<int>(n, -1));
        return numOfTrees(1, n, memo);
    }
private:
    int numOfTrees(const int& start, const int& end, vector<vector<int>>& memo) {
        if (start >= end) return 1;
        if (memo[start - 1][end - 1] != -1) return memo[start - 1][end - 1];
        int res = 0;
        for (int i = start; i <= end; i++) {
            int leftNumOfTrees = numOfTrees(start, i - 1, memo);
            int rightNumOfTrees = numOfTrees(i + 1, end, memo);
            res += leftNumOfTrees * rightNumOfTrees;
        }
        memo[start - 1][end - 1] = res;
        return res;
    }
};
```

