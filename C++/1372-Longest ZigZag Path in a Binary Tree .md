https://leetcode.com/problems/longest-zigzag-path-in-a-binary-tree/

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
// calculate the len of nodes in longest ZigZag path (res), 
// then the path length is len - 1 (res - 1).
class Solution {
public:
    int longestZigZag(TreeNode* root) {
        int res = 1;
        dfs(root->left, true, 1, res);
        dfs(root->right, false, 1, res);
        return res - 1;
    }
private:
    // drirection => {[left == true], [right == false]}
    void dfs(TreeNode* node, bool direction, int len, int& res) {
        if (node == nullptr) return;
        res = max(res, len + 1);
        if (direction) { // 从上一个节点的左分支来到当前节点
            dfs(node->left, true, 1, res);
            dfs(node->right, false, len + 1, res);
        } else {         // 从上一个节点的右分支来到当前节点
            dfs(node->left, true, len + 1, res);
            dfs(node->right, false, 1, res);
        }
    }
};
```

