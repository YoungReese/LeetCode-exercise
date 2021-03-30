https://leetcode.com/problems/validate-binary-search-tree/

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
// the function helper like inorder traversal, each step compare the node with it's preNode in value
class Solution {
public:
    bool isValidBST(TreeNode* root) {
        TreeNode* preNode = nullptr;
        bool res = true;
        helper(root, preNode, res);
        return res;
    }
private:
    void helper(TreeNode* node, TreeNode*& preNode, bool& res) { // left - middle - right
        if (node == nullptr) return;
        helper(node->left, preNode, res);
        if (preNode != nullptr && node->val <= preNode->val) {
            res = false;
            return;
        }
        preNode = node;
        helper(node->right, preNode, res);
    }
};
```

