https://leetcode.com/problems/binary-tree-maximum-path-sum/

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
// Given the root of a binary tree, return the maximum path sum of any path.
class Solution {
public:
    int maxPathSum(TreeNode* root) {
        int res = INT_MIN;
        helper(root, res);
        return res;
    }
private:
    int helper(TreeNode* node, int& res) {
        if (node == nullptr) return 0;
        int leftMaxVal = max(0, helper(node->left, res));
        int rightMaxVal = max(0, helper(node->right, res));
        res = max(res, node->val + leftMaxVal + rightMaxVal);
        return node->val + (leftMaxVal > rightMaxVal ? leftMaxVal : rightMaxVal);
    }
}; 
```

