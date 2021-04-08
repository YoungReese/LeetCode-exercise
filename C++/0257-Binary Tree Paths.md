https://leetcode.com/problems/binary-tree-paths/

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
    vector<string> binaryTreePaths(TreeNode* root) {
        vector<string> res;
        dfs(root, "", res);
        return res;
    }
private:
    void dfs(TreeNode* node, string s, vector<string>& res) {
        if (node == nullptr) return;
        
        s += to_string(node->val);
        if (node->left == node->right) {
            res.push_back(s);
            return;
        }
        s += "->";
        
        dfs(node->left, s, res);
        dfs(node->right, s, res);
    }
};
```
