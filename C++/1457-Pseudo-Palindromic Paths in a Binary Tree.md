https://leetcode.com/problems/pseudo-palindromic-paths-in-a-binary-tree/

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
// Constraints:
// The number of nodes in the tree is in the range [1, 105].
// 1 <= Node.val <= 9
// 用一个变量 path 的1到9位（最低位记做0位）表示数字1到9
// 每次将数字对应位进行异或，碰到叶子结点时判断 (path & (path - 1)) == 0，表示最多只有一个位置有1
// 成立表示这是一个可以通过排列变成回文串，即伪回文串
class Solution {
public:
    int pseudoPalindromicPaths (TreeNode* root) {
        int res = 0;
        dfs(root, 0, res);
        return res;
    }
private:
    void dfs(TreeNode* node, int path, int& res) {
        if (node == nullptr) return;
        path = path ^ (1 << node->val);
        if (node->left == node->right) { // node 是叶子结点的特性
            if ((path & (path - 1)) == 0) {
                res++;
            }
        } 
        dfs(node->left, path, res);
        dfs(node->right, path, res);
    }
};
```

