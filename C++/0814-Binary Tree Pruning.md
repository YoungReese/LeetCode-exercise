https://leetcode.com/problems/binary-tree-pruning/

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
    TreeNode* pruneTree(TreeNode* root) {
        return hasOneInTree(root) ? root : nullptr;
    }
private:
    bool hasOneInTree(TreeNode* node) { // postorder
        if (node == nullptr) return false;
        bool leftHasOne = hasOneInTree(node->left);
        bool rightHasOne = hasOneInTree(node->right);
        if (!leftHasOne) {
            delete node->left;
            node->left = nullptr;
        }
        if (!rightHasOne) {
            delete node->right;
            node->right = nullptr;
        }
        return node->val || leftHasOne || rightHasOne;
    }
};
```



