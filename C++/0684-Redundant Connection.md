https://leetcode.com/problems/redundant-connection/

```c++
class Solution {
public:
    vector<int> findRedundantConnection(vector<vector<int>>& edges) {
        int n = edges.size();
        vector<int> parent(n + 1, -1);
        vector<int> res(2);
        for (int i = 0; i < n; i++) {
            int u = edges[i][0], v = edges[i][1];
            int rootOfU = myFind(u, parent), rootOfV = myFind(v, parent);
            if (rootOfU == rootOfV) { res[0] = u; res[1] = v; }
            else myUnion(rootOfU, rootOfV, parent);
        }
        return res;
    }
private:
    void myUnion(int root1, int root2, vector<int>& parent) {
        if (parent[root1] < parent[root2]) {          // 按秩归并
            parent[root1] += parent[root2];
            parent[root2] = root1;
        } else {
            parent[root2] += parent[root1];
            parent[root1] = root2;
        }
    }
    
    int myFind(int x, vector<int>& parent) {
        if (parent[x] < 0) return x;
        return parent[x] = myFind(parent[x], parent); // 路经压缩
    }
};
```
