https://leetcode.com/problems/sum-root-to-leaf-numbers/

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
    int sumNumbers(TreeNode* root) {
        return helper(root, 0);
    }
private:
    int helper(TreeNode* node, int cur) {
        if (node == nullptr) return cur;
        cur = cur * 10 + node->val;
        if (node->left == node->right) return cur;
        int leftSum = node->left ? helper(node->left, cur) : 0;
        int rightSum = node->right ? helper(node->right, cur) : 0;
        return leftSum + rightSum;
    } 
};
```

