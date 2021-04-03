https://leetcode.com/problems/binary-tree-level-order-traversal-ii/

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
    vector<vector<int>> levelOrderBottom(TreeNode* root) {
        if (root == nullptr) return {};
        
        queue<TreeNode*> q;
        q.push(root);
        int level = getMaxDepth(root);
        vector<vector<int>> res(level);
        TreeNode* node;
        while (!q.empty()) {
            vector<int> vec;
            for (int i = 0, n = q.size(); i < n; i++) {
                node = q.front(); q.pop();
                vec.push_back(node->val);
                if (node->left) q.push(node->left);
                if (node->right) q.push(node->right);
            }
            res[--level] = vec;
        }
        
        return res;
    }
private:
    int getMaxDepth(TreeNode* node) {
        if (node == nullptr) return 0;
        return max(getMaxDepth(node->left), getMaxDepth(node->right)) + 1;
    }
};
```

