https://leetcode.com/problems/maximum-depth-of-n-ary-tree/

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
    int maxDepth(Node* root) {
        if (root == nullptr) return 0;
        queue<Node*> q;
        q.push(root);
        int depth = 0;
        while (!q.empty()) {
            depth++;
            Node* node;
            for (int i = 0, n = q.size(); i < n; i++) {
                node = q.front(); q.pop();
                for (auto& child : node->children) {
                    if (child) q.push(child);
                }
            }
        }
        return depth;
    }
};
```



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
    int maxDepth(Node* root) {
        if (root == nullptr) return 0;
        int maxSubTreeDepth = 0;
        for (auto& child : root->children) {
            maxSubTreeDepth = max(maxSubTreeDepth, maxDepth(child));
        }
        return maxSubTreeDepth + 1;
    }
};
```



