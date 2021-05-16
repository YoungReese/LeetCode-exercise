https://leetcode.com/problems/word-search/

```c++
class Solution {
public:
    bool exist(vector<vector<char>>& board, string word) {
        int m = board.size(), n = board[0].size();
        vector<vector<bool>> visited(m, vector<bool>(n, false));
        bool find = false;
        for (int i = 0; i < m; ++i) {
            for (int j = 0; j < n; ++j) {
                if (find) return find;
                dfs(board, visited, m, n, i, j, word, 0, find);
            }
        }
        return find;
    }
private:
    void dfs(vector<vector<char>>& board, vector<vector<bool>>& visited, 
             int& m, int& n, int x, int y, string& word, int pos, bool& find) {
        
        if (x < 0 || y < 0 || x == m || y == n || find) return;
        if (visited[x][y] || board[x][y] != word[pos]) return;
        if (pos == word.size() - 1) {
            find = true;
            return;
        }
        
        visited[x][y] = true;
        dfs(board, visited, m, n, x, y - 1, word, pos + 1, find);
        dfs(board, visited, m, n, x - 1, y, word, pos + 1, find);
        dfs(board, visited, m, n, x, y + 1, word, pos + 1, find);
        dfs(board, visited, m, n, x + 1, y, word, pos + 1, find);
        visited[x][y] = false;
    }
};
```



```c++
// optimized: not use the visited
// board and word consists of only lowercase and uppercase English letters.
class Solution {
public:
    bool exist(vector<vector<char>>& board, string word) {
        int m = board.size(), n = board[0].size();
        bool find = false;
        for (int i = 0; i < m; ++i) {
            for (int j = 0; j < n; ++j) {
                if (find) return find;
                dfs(board, m, n, i, j, word, 0, find);
            }
        }
        return find;
    }
private:
    void dfs(vector<vector<char>>& board, const int& m, const int& n, 
             int x, int y, string& word, int pos, bool& find) {
        
        if (x < 0 || y < 0 || x == m || y == n || find || board[x][y] != word[pos]) return;
        if (pos == word.size() - 1) {
            find = true;
            return;
        }
        char tmp = board[x][y];
        board[x][y] = '#';
        dfs(board, m, n, x, y - 1, word, pos + 1, find);
        dfs(board, m, n, x - 1, y, word, pos + 1, find);
        dfs(board, m, n, x, y + 1, word, pos + 1, find);
        dfs(board, m, n, x + 1, y, word, pos + 1, find);
        board[x][y] = tmp;
    }
};
```

