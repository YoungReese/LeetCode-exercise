https://leetcode.com/problems/diameter-of-binary-tree/

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
    int diameterOfBinaryTree(TreeNode* root) {
        int res = 0;
        getHeight(root, res);
        return res;
    }
private:
    int getHeight(TreeNode* node, int& res) { // postorder
        if (node == nullptr) return 0;
        int leftHeight = getHeight(node->left, res);
        int rightHeight = getHeight(node->right, res);
        res = max(res, leftHeight + rightHeight);
        return 1 + (leftHeight > rightHeight ? leftHeight : rightHeight);
    }
};
```



