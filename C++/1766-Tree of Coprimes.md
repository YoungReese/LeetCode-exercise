https://leetcode.com/problems/tree-of-coprimes/

```c++
// O(50 * n)  O(n)
// path[nums[cur]].emplace_back(cur, depth);  <=>
// path[nums[cur]].push_back(make_pair(cur, depth)); <=>
// path[nums[cur]].push_back(pair<int, int>(cur, depth));
class Solution {
public:
    vector<int> getCoprimes(vector<int>& nums, vector<vector<int>>& edges) {
        const int n = nums.size();
        const int LIMIT = 50 + 1;
        
        vector<vector<int>> g(n);
        for (auto& e : edges) {
            g[e[0]].push_back(e[1]);
            g[e[1]].push_back(e[0]);
        }
        
        vector<vector<int>> coprime(LIMIT);
        for (int i = 1; i < LIMIT; i++) {
            for (int j = 1; j < LIMIT; j++) {
                if (gcd(i, j) == 1) coprime[i].push_back(j);
            }
        }        
        
        // 初始值全部存储INT_MAX, 表示没有被更新过
        vector<int> res(n, INT_MAX);
        // 存储节点数字nums[cur]在nums中的角标位置cur和在树中的深度depth（1 <= nums[cur] <= 50）
        // 不断的dfs，因为数字会有大量重复，深度递进，相同数字会被添加到尾部，递进退出时从尾部弹出
        vector<vector<pair<int, int>>> path(LIMIT);
        
        function<void(int, int)> dfs = [&] (int cur, int depth) {
            int max_depth = -1, ancestor = -1;
            for (const int& x : coprime[nums[cur]]) {
                if (!path[x].empty() && path[x].back().second > max_depth) {
                    max_depth = path[x].back().second;
                    ancestor = path[x].back().first;
                }
            }
            res[cur] = ancestor;
            path[nums[cur]].emplace_back(cur, depth);
            
            for (int next : g[cur]) if (res[next] == INT_MAX) dfs(next, depth + 1);
            
            path[nums[cur]].pop_back();
        };
        
        dfs(0, 0);
        return res;
    }
};
```

