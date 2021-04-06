https://leetcode.com/problems/binary-tree-postorder-traversal/

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
class Solution { // 左 - 右 - 根
public:
    vector<int> postorderTraversal(TreeNode* root) {
        vector<int> res;
        postorder(root, res);
        return res;
    }
private:
    void postorder(TreeNode* node, vector<int>& res) {
        if (node == nullptr) return;
        postorder(node->left, res);
        postorder(node->right, res);
        res.push_back(node->val);
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
class Solution { // 左 - 右 - 根
public:
    vector<int> postorderTraversal(TreeNode* root) {
        if (root == nullptr) return {};      
        TreeNode* node = root;
        vector<int> res;
        stack<TreeNode*> stk;
        TreeNode* pre = nullptr;
        while (!stk.empty() || node) {
            while (node) {
                stk.push(node);
                node = node->left;
            }
            node = stk.top(); stk.pop();
            if (node->right == nullptr || node->right == pre) {
                res.push_back(node->val);
                pre = node;
                node = nullptr;
            } else {
                stk.push(node);
                node = node->right;
            } 
        }
        return res;
    }
};
```

