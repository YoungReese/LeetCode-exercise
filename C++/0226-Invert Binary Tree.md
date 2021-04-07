https://leetcode.com/problems/invert-binary-tree/

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
// postorder
class Solution {
public:
    TreeNode* invertTree(TreeNode* root) {
        return invert(root);
    }
private:
    TreeNode* invert(TreeNode* node) {
        if (node == nullptr) return node;
        TreeNode* leftNode = invert(node->left);
        TreeNode* rightNode = invert(node->right);
        node->left = rightNode;
        node->right = leftNode;
        return node;
    }
};
```
