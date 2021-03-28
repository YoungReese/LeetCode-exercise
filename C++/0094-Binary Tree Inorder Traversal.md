https://leetcode.com/problems/binary-tree-inorder-traversal/

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
// recursive
class Solution {
public:
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> res;
        inorder(root, res);
        return res;
    }
private:
    void inorder(TreeNode* node, vector<int>& res) {
        if (node == nullptr) return;
        inorder(node->left, res);
        res.push_back(node->val);
        inorder(node->right, res);
    }
};
```



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
// iteration
class Solution {
public:
    vector<int> inorderTraversal(TreeNode* root) {
        stack<TreeNode*> stk;
        vector<int> res;
        TreeNode* node = root;
        while (!stk.empty() || node) {
            while (node) {
                stk.push(node);
                node = node->left;
            }
            if (node == nullptr) {
                node = stk.top();
                stk.pop();
            }
            res.push_back(node->val);
            node = node->right;
        }
        return res;
    }
};
```

