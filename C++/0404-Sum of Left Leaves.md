https://leetcode.com/problems/sum-of-left-leaves/

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
    int sumOfLeftLeaves(TreeNode* root) {
        int res = 0;
        dfs(root, false, res);
        return res;
    }
private:
    void dfs(TreeNode* node, bool fromLeft, int& sum) {
        if (node == nullptr) return;
        if (fromLeft && node->left == node->right) sum += node->val;
        dfs(node->left, true, sum);
        dfs(node->right, false, sum);
    }
};
```


