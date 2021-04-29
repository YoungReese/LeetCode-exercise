https://leetcode.com/problems/number-of-provinces/

```c++
class Solution {
public:
    int findCircleNum(vector<vector<int>>& isConnected) {
        int n = isConnected.size();
        vector<bool> visited(n, false);
        int province = 0;
        for (int i = 0; i < n; ++i) {
            if (!visited[i]) {
                dfs(isConnected, i, visited);
                ++province;
            }
        }
        return province;
    }
private:
    void dfs(vector<vector<int>>& isConnected, int i, vector<bool>& visited) {
        visited[i] = true;
        for (int k = 0; k < isConnected.size(); ++k) {
            if (isConnected[i][k] && !visited[k]) 
                dfs(isConnected, k, visited);
        }
    }
};
```


