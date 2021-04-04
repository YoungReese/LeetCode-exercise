https://leetcode.com/problems/balanced-binary-tree/

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
    bool isBalanced(TreeNode* root) {
        if (root == nullptr) return true;
        bool res = true;
        getMaxDepth(root, res);
        return res;
    }
private:
    int getMaxDepth(TreeNode* node, bool& res) {
        if (node == nullptr) return 0;
        
        int leftMaxDepth, rightMaxDepth;
        if (res) leftMaxDepth = getMaxDepth(node->left, res);
        if (res) rightMaxDepth = getMaxDepth(node->right, res);
        if (res && abs(leftMaxDepth - rightMaxDepth) > 1) res = false;
        
        return res ? (1 + max(leftMaxDepth, rightMaxDepth)) : -1;
    }
};
```

