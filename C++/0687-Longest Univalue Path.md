https://leetcode.com/problems/longest-univalue-path/

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
    int longestUnivaluePath(TreeNode* root) {
        int res = 0;
        arrowLength(root, res);
        return res;
    }
private:
    int arrowLength(TreeNode* node, int& res) {
        if (node == nullptr || node->left == node->right) return 0;
        
        int leftLen = arrowLength(node->left, res);
        int rightLen = arrowLength(node->right, res);
        
        int leftRes = 0, rightRes = 0;
        if (node->left && node->left->val == node->val) leftRes = leftLen + 1;
        if (node->right && node->right->val == node->val) rightRes = rightLen + 1;
        res = max(res, leftRes + rightRes);
        
        return max(leftRes, rightRes);
    }
};
```
