https://leetcode.com/problems/leaf-similar-trees/

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
    bool leafSimilar(TreeNode* root1, TreeNode* root2) {
        vector<int> vec1, vec2;
        dfs(root1, vec1);
        dfs(root2, vec2);
        return vec1 == vec2;
    }
private:
    void dfs(TreeNode* node, vector<int>& vec) {
        if (node == nullptr) return;
        if (node->left == node->right) vec.push_back(node->val);
        dfs(node->left, vec);
        dfs(node->right, vec);
    }
};
```
