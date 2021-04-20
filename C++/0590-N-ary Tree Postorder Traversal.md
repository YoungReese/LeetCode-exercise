https://leetcode.com/problems/n-ary-tree-postorder-traversal/

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
    vector<int> postorder(Node* root) {
        vector<int> res;
        helper(root, res);
        return res;
    }
private:
    void helper(Node* node, vector<int>& res) {
        if (node == nullptr) return;
        for (Node*& child : node->children) helper(child, res);
        res.push_back(node->val);
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
    vector<int> postorder(Node* root) {
        if (root == nullptr) return {};
        
        vector<int> res;
        Node* pre = nullptr;
        stack<Node*> stk;
        stk.push(root);
        Node* node;
        while (!stk.empty()) {
            node = stk.top(); stk.pop();
            
            if (node != nullptr) {
                int last = node->children.size() - 1;
                if (last < 0 || node->children[last] == pre) {
                    res.push_back(node->val);
                    pre = node;
                } else {
                    stk.push(node);
                    for (int i = node->children.size() - 1; i >= 0; i--) {
                        stk.push(node->children[i]);
                    }
                }
            }
        }
        
        return res;
    }
};
```

