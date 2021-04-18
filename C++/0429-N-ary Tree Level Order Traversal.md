https://leetcode.com/problems/n-ary-tree-level-order-traversal/

```c++
/*
// Definition for a Node.
class Node {
public:
    int val;
    vector<Node*> children;

    Node() {}

    Node(int _val) {
        val = _val;
    }

    Node(int _val, vector<Node*> _children) {
        val = _val;
        children = _children;
    }
};
*/
class Solution {
public:
    vector<vector<int>> levelOrder(Node* root) {
        if (root == nullptr) return {};
        vector<vector<int>> res;
        queue<Node*> q;
        q.push(root);
        while (!q.empty()) {
            Node* node;
            vector<int> v;
            for (int i = 0, n = q.size(); i < n; i++) {
                node = q.front(); q.pop();
                v.push_back(node->val);
                for (auto& child : node->children) {
                    if (child) q.push(child);
                }
            }
            res.push_back(v);
        }
        return res;
    }
};
```


