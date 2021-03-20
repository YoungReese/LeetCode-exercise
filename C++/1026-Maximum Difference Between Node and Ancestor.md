https://leetcode.com/problems/maximum-difference-between-node-and-ancestor/

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
// pay attention to every path from root node to leaf node, 
// choose the maxVal and the minVal in every path, that's the core
class Solution {
public:
    int maxAncestorDiff(TreeNode* root) {
        int res = 0;
        dfs(root, root->val, root->val, res);
        return res;
    }
private:
    void dfs(TreeNode* node, int maxVal, int minVal, int& res) {
        if (node == nullptr) return;
        
        maxVal = max(maxVal, node->val);
        minVal = min(minVal, node->val);
        
        if (node->left == node->right) { // leaf node
            res = max(res, maxVal - minVal);
        }
        
        dfs(node->left, maxVal, minVal, res);
        dfs(node->right, maxVal, minVal, res);
    }
};
```

