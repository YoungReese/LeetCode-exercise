https://leetcode.com/problems/max-area-of-island/

```c++
class Solution {
public:
    int maxAreaOfIsland(vector<vector<int>>& grid) {
        int m = grid.size(), n = grid[0].size();
        vector<vector<bool>> visited(m, vector<bool>(n, false));
        int res = 0;
        for (int row = 0; row < m; ++row) {
            for (int col = 0; col < n; ++col) {
                if (grid[row][col] && !visited[row][col]) 
                    res = max(res, dfs(grid, m, n, visited, row, col));
            }
        }
        return res;
    }
private:
    int dfs(const vector<vector<int>>& grid, const int& m, const int& n, 
            vector<vector<bool>>& visited, int row, int col) {
        
        if (!grid[row][col]) return 0;
        
        visited[row][col] = true;
        int area = 1;
        if (row > 0 && !visited[row - 1][col]) area += dfs(grid, m, n, visited, row - 1, col);
        if (row < m - 1 && !visited[row + 1][col]) area += dfs(grid, m, n, visited, row + 1, col);
        if (col > 0 && !visited[row][col - 1]) area += dfs(grid, m, n, visited, row, col - 1);
        if (col < n - 1 && !visited[row][col + 1]) area += dfs(grid, m, n, visited, row, col + 1);
        
        return area;
    }
};
```



```c++
class Solution {  // non-empty 2D array grid
public:
    int maxAreaOfIsland(vector<vector<int>>& grid) {
        int m = grid.size();
        int n = grid[0].size();
        vector<vector<bool>> visited(m, vector<bool>(n, false));
        int res = 0;
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (grid[i][j] == 0 || visited[i][j]) continue;
                res = max(res, dfs(grid, visited, m, n, i, j));
            }
        }
        return res;     
    }
private:
    int dfs(const vector<vector<int>>& grid, vector<vector<bool>>& visited, 
            const int& m, const int& n, int row, int col) {
        visited[row][col] = true;
        if (grid[row][col] == 0) return 0;
        int maxAera = 1;
        // up
        if (row > 0 && !visited[row - 1][col]) {
            maxAera += dfs(grid, visited, m, n, row - 1, col);
        }
        // right
        if (col < n - 1 && !visited[row][col + 1]) {
            maxAera += dfs(grid, visited, m, n, row, col + 1);
        }
        // down
        if (row < m - 1 && !visited[row + 1][col]) {
            maxAera += dfs(grid, visited, m, n, row + 1, col);
        }
        // left
        if (col > 0 && !visited[row][col - 1]) {
            maxAera += dfs(grid, visited, m, n, row, col - 1);
        }
        return maxAera;
    }
};
```