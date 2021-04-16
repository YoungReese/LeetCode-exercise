https://leetcode.com/problems/minimum-distance-between-bst-nodes/

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
    int minDiffInBST(TreeNode* root) {
        int prev = -1;
        int diff = INT_MAX;
        inorder(root, prev, diff);
        return diff;
    }
private:
    void inorder(TreeNode* node, int& prev, int& diff) {
        if (node == nullptr) return;
        inorder(node->left, prev, diff);
        if (prev >= 0) diff = min(diff, node->val - prev);
        prev = node->val;
        inorder(node->right, prev, diff);
    }
};
```



