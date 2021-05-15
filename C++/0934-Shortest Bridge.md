https://leetcode.com/problems/shortest-bridge/

```c++
// 2 <= grid.length == grid[0].length <= 100
// 通过 dfs 找到第一个岛屿，将岛屿的 1 改成 2 并放入 q
// 使用 q 进行 bfs，遇到 2 说明访问过，遇到 1 表示此时建立的就是最短桥，
// 遇到 0 加入队列并改为 2，一轮队列访问完毕，++res，进行下一轮
class Solution {
public:
    int shortestBridge(vector<vector<int>>& grid) {
        int n = grid.size();
        queue<pair<int, int>> q;
        int flipped = false;
        for (int i = 0; i < n; ++i) {
            for (int j = 0; j < n; ++j) {
                if (grid[i][j] == 1) {
                    dfs(grid, q, n, i, j);
                    flipped = true;
                    break;
                }
            }
            if (flipped) break;
        }
        
        int res = 1;
        while (!q.empty()) {
            for (int i = 0, cnt = q.size(); i < cnt; ++i) {
                auto [x, y] = q.front(); q.pop();
                for (int k = 0; k < 4; ++k) {
                    int newX = x + dir[k][0], newY = y + dir[k][1];
                    if (isValid(newX, newY, n)) {
                        if (grid[newX][newY] == 2) continue;
                        if (grid[newX][newY] == 1) return res;
                        q.push({newX, newY});
                        grid[newX][newY] = 2;
                    }
                }
            }
            ++res;
        }
        return 1;
    }
private:
    int dir[4][2] = {{0, -1}, {-1, 0}, {0, 1}, {1, 0}};
    
    void dfs(vector<vector<int>>& grid, queue<pair<int, int>>& q, int& n, int x, int y) {
        if (!isValid(x, y, n) || grid[x][y] == 2) return;
        if (grid[x][y] == 0) {
            q.push({x, y});
            return;
        }
        grid[x][y] = 2;
        
        for (int k = 0; k < 4; ++k) dfs(grid, q, n, x + dir[k][0], y + dir[k][1]);
    }
    
    bool isValid(int& x, int& y, int& n) {
        if (x < 0 || y < 0 || x == n || y == n) return false;
        return true;
    }
};
```

