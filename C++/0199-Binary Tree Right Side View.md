https://leetcode.com/problems/binary-tree-right-side-view/

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
class Solution {
public:
    vector<int> rightSideView(TreeNode* root) {
        if (root == nullptr) return {};
        
        vector<int> res;
        queue<TreeNode*> q;
        q.push(root);
        
        while (!q.empty()) {
            int n = q.size();
            TreeNode* node;
            for (int i = 0; i < n; i++) {
                node = q.front(); q.pop();
                if (node->left) q.push(node->left);
                if (node->right) q.push(node->right);
            }
            res.push_back(node->val);
        }
        
        return res;
    }
};
```
