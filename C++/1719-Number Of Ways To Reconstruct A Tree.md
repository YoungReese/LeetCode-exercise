https://leetcode.com/problems/number-of-ways-to-reconstruct-a-tree/

```c++
class Solution {
public:
    int checkWays(vector<vector<int>>& pairs) { // There are no duplicates and xi < yi.
        
        vector<vector<int>> g(501);
        vector<int> count(501, 0);
        for (const auto& pair : pairs) { // 1 <= xi < yi <= 500
            count[pair[0]]++;
            count[pair[1]]++;
            g[pair[0]].push_back(pair[1]);
            g[pair[1]].push_back(pair[0]);
        }
        
        vector<int> array; // 记录有哪些value
        for (int i = 1; i < 501; i++) {
            if (count[i] == 0) continue;
            array.push_back(i);
        }
        int n = array.size(); // array中的数字个数就是节点数字
        // 将节点数字按照节点的度进行降序排序，因此 array[0] 是根结点的数值
        sort(array.begin(), 
             array.end(), 
             [&] (const int& x, const int& y) { return count[x] - count[y] > 0; });

        // 排序后 count[array[0]] 是最多的，如果可见建树那么值一定为 n - 1
        if (count[array[0]] != n - 1) return 0;
        
        // 定义 par[x] 为目前已知的 x 的最近祖先
        vector<int> par(501, -1);
        
        vector<bool> visited(501, false);
        
        bool flag = false;
        for (int i = 0; i < n; i++) {
            int u = array[i];
            for (int j = 0, len = g[u].size(); j < len; j++) {
                int v = g[u][j];
                if (count[u] == count[v]) flag = true;
                if (!visited[v]) {
                    if (par[v] != par[u]) return 0;
                    par[v] = u;
                }
            }
            visited[u] = true;
        }
        
        return flag ? 2 : 1;
    }
};
```

[参考资料](https://leetcode-cn.com/problems/number-of-ways-to-reconstruct-a-tree/solution/onmde-luan-gao-zuo-fa-by-weak-chicken-y2mv/)

