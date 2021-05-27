https://leetcode.com/problems/range-sum-query-2d-immutable/

```c++
// 注：leetcode 的测试集更新过导致运行时间只打败了约 5% 的提交
// build sumMatrix takes O(mn) and sumRegion takes O(1)
class NumMatrix {
public:
    NumMatrix(vector<vector<int>>& matrix) {
        int m = matrix.size(), n = matrix[0].size();
        sumMatrix = vector<vector<int>>(m + 1, vector<int>(n + 1, 0));
        for (int i = 1; i <= m; ++i) {
            for (int j = 1; j <= n; ++j) {
                sumMatrix[i][j] = sumMatrix[i - 1][j] + sumMatrix[i][j - 1]
                                - sumMatrix[i - 1][j - 1] + matrix[i - 1][j - 1];
            }
        }
    }
    
    int sumRegion(int row1, int col1, int row2, int col2) {
        return sumMatrix[row2 + 1][col2 + 1] - sumMatrix[row2 + 1][col1]
               - sumMatrix[row1][col2 + 1] + sumMatrix[row1][col1];
    }
private:
    vector<vector<int>> sumMatrix;
};

/**
 * Your NumMatrix object will be instantiated and called as such:
 * NumMatrix* obj = new NumMatrix(matrix);
 * int param_1 = obj->sumRegion(row1,col1,row2,col2);
 */
```

