https://leetcode.com/problems/second-minimum-node-in-a-binary-tree/

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
// root.val = min(root.left.val, root.right.val) always holds.
// 1 <= Node.val <= 2^31 - 1
class Solution {
public:
    int findSecondMinimumValue(TreeNode* root) {
        int firstMin = root->val, secondMin = -1;
        dfs(root, firstMin, secondMin);
        return secondMin;
    }
private:
    void dfs(TreeNode* node, int& firstMin, int& secondMin) {
        if (node == nullptr) return;
        if (node->val > firstMin && (secondMin == -1 || node->val < secondMin)) 
            secondMin = node->val;
        dfs(node->left, firstMin, secondMin);
        dfs(node->right, firstMin, secondMin);
    }
};
```

