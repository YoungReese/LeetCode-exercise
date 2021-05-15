https://leetcode.com/problems/pacific-atlantic-water-flow/

```c++
class Solution {
public:
    vector<vector<int>> pacificAtlantic(vector<vector<int>>& heights) {
        int m = heights.size(), n = heights[0].size();
        vector<vector<bool>> reachPacific(m, vector<bool>(n, false));
        vector<vector<bool>> reachAtlantic(m, vector<bool>(n, false));
        
        for (int i = 0; i < m; ++i) {
            dfs(heights, m, n, reachPacific, i, 0);
            dfs(heights, m, n, reachAtlantic, i, n - 1);
        }
        
        for (int j = 0; j < n; ++j) {
            dfs(heights, m, n, reachPacific, 0, j);
            dfs(heights, m, n, reachAtlantic, m - 1, j);
        }
        
        vector<vector<int>> res;
        for (int i = 0; i < m; ++i) {
            for (int j = 0; j < n; ++j) {
                if (reachPacific[i][j] && reachAtlantic[i][j]) res.push_back({i, j});
            }
        }
        
        return res;
    }
private:
    int dir[4][2] = {{0, -1}, {-1, 0}, {0, 1}, {1, 0}};
    void dfs(vector<vector<int>>& heights, int& m, int& n,
             vector<vector<bool>>& reach, int x, int y) {
        
        if (reach[x][y]) return;
        reach[x][y] = true;
        for (int k = 0; k < 4; ++k) {
            int newX = x + dir[k][0], newY = y + dir[k][1];
            if (isValid(newX, newY, m, n) && heights[newX][newY] >= heights[x][y]) {
                dfs(heights, m, n, reach, newX, newY);
            }
        }
    }
    
    bool isValid(int& x, int& y, int& m, int& n) {
        if (x < 0 || y < 0 || x == m || y == n) return false;
        return true;
    }
};
```


