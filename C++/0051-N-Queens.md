https://leetcode.com/problems/n-queens/

```c++
// ldiag => 逆时针：左上角 0
// rdiag => 逆时针：左下角 0
class Solution {
public:
    vector<vector<string>> solveNQueens(int n) {
        vector<bool> col(n, false), ldiag(2 * n - 1, false), rdiag(2 * n - 1, false);
        vector<string> board(n, string(n, '.'));
        vector<vector<string>> res;
        backtracking(0, n, col, ldiag, rdiag, board, res);
        return res;
    }
private:
    void backtracking(int row, const int& n, vector<bool>& col, 
                      vector<bool>& ldiag, vector<bool>& rdiag,
                      vector<string>& board, vector<vector<string>>& res) {
        
        if (row == n) {
            res.push_back(board);
            return;
        }
        
        for (int j = 0; j < n; ++j) {
            if (col[j] || ldiag[row + j] || rdiag[n - row - 1 + j]) continue;
            board[row][j] = 'Q';
            col[j] = ldiag[row + j] = rdiag[n - row - 1 + j] = true;                              
            backtracking(row + 1, n, col, ldiag, rdiag, board, res);                             
            board[row][j] = '.';
            col[j] = ldiag[row + j] = rdiag[n - row - 1 + j] = false;
        }
    }
};
```

