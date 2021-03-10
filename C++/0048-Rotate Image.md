https://leetcode.com/problems/rotate-image/

```c++
// 行列交错
// (0,2)-(0,2)-(2,2)-(2,0)-(0,0)
// O(M) in-place, M is the cells of matrix
class Solution {
public:
    void rotate(vector<vector<int>>& matrix) {
        int n = matrix.size();
        for (int i = 0; i < n / 2; i++) {           // 行
            for (int j = i; j < n - i - 1; j++) {   // 列
                int tmp = matrix[i][j];        
                matrix[i][j] = matrix[n - j - 1][i];       
                matrix[n - j - 1][i] = matrix[n - i - 1][n - j - 1];
                matrix[n - i - 1][n - j - 1] = matrix[j][n - i - 1];
                matrix[j][n - i - 1] = tmp;
            }
        }
    }
};
```

