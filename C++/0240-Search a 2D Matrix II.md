https://leetcode.com/problems/search-a-2d-matrix-ii/

```c++
// 选择最右上角的位置或者最左下角的点都可
// 这个点的特点是所在行列中对应的最大数值或最小数值
class Solution {
public:
    bool searchMatrix(vector<vector<int>>& matrix, int target) {
        int m = matrix.size(), n = matrix[0].size();
        int row = 0, col = n - 1;
        while (row < m && col >= 0) {
            if (matrix[row][col] == target) return true;
            if (matrix[row][col] < target) ++row;
            else --col;
        }
        return false;
    }
};
```

