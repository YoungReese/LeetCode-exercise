https://leetcode.com/problems/complete-binary-tree-inserter/

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
// The initial given tree is complete and contains between 1 and 1000 nodes.
class CBTInserter {
public:
    CBTInserter(TreeNode* root) {
        this->root = root;
        queue<TreeNode*> q;
        q.push(root);
        while (!q.empty()) {
            TreeNode* node = q.front(); q.pop();
            if (!(node->left && node->right)) que.push(node);
            if (node->left) q.push(node->left);
            if (node->right) q.push(node->right);
        }
    }
    
    int insert(int v) {
        que.push(new TreeNode(v));
        TreeNode* parent = que.front();
        if (parent->left == nullptr) {
            parent->left = que.back();
        } else {
            parent->right = que.back();
            que.pop();
        }
        return parent->val;
    }
    
    TreeNode* get_root() {
        return root;
    }
private:
    TreeNode* root;       // record the root.
    queue<TreeNode*> que; // save the nodes that have 0 or 1 children, in number order. (bfs)
};

/**
 * Your CBTInserter object will be instantiated and called as such:
 * CBTInserter* obj = new CBTInserter(root);
 * int param_1 = obj->insert(v);
 * TreeNode* param_2 = obj->get_root();
 */
```

