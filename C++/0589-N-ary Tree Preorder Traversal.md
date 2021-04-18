https://leetcode.com/problems/n-ary-tree-preorder-traversal/

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
    vector<int> preorder(Node* root) {
        vector<int> res;
        dfs(root, res);
        return res;
    }
private:
    void dfs(Node* node, vector<int>& res) {
        if (node == nullptr) return;
        res.push_back(node->val);
        for (auto& child : node->children) dfs(child, res);
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
// 栈模拟
class Solution {
public:
    vector<int> preorder(Node* root) {
        if (root == nullptr) return {};
        
        stack<Node*> stk;
        stk.push(root);
        vector<int> res;
        
        while (!stk.empty()) {
            Node* node = stk.top(); stk.pop();
            if (node != nullptr) {
                res.push_back(node->val);
                for (int i = node->children.size() - 1; i >= 0; i--) {
                    stk.push(node->children[i]);
                }
            }
        }
        
        return res;
    }
};
```

