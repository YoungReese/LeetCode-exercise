https://leetcode.com/problems/binary-tree-preorder-traversal/

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
    vector<int> preorderTraversal(TreeNode* root) {
        vector<int> res;
        preorder(root, res);
        return res;
    }
private:
    void preorder(TreeNode* node, vector<int>& res) {
        if (node == nullptr) return;
        res.push_back(node->val);
        preorder(node->left, res);
        preorder(node->right, res);
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
class Solution { // 根 - 左 - 右
public:
    vector<int> preorderTraversal(TreeNode* root) {
        if (root == nullptr) return {};
        
        vector<int> res;
        TreeNode* node = root;
        stack<TreeNode*> stk;

        while (!stk.empty() || node) {
            while (node) {
                res.push_back(node->val);
                stk.push(node);
                node = node->left;
            }
            node = stk.top(); stk.pop();
            node = node->right;
        }
        
        return res;
    }
};
```

