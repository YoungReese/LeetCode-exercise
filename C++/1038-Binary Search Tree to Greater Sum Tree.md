https://leetcode.com/problems/binary-search-tree-to-greater-sum-tree/

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
    TreeNode* bstToGst(TreeNode* root) {
        int sum = 0;
        rightRootLeft(root, sum);
        return root;
    }
private:
    void rightRootLeft(TreeNode* node, int& sum) {
        if (node == nullptr) return;
        rightRootLeft(node->right, sum);
        node->val += sum;
        sum = node->val;
        rightRootLeft(node->left, sum);            
    }
};
```



