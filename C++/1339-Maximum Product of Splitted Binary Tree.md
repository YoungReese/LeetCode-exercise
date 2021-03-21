https://leetcode.com/problems/maximum-product-of-splitted-binary-tree/

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
    int maxProduct(TreeNode* root) {
        dfs(root);
        long long res = 0;
        calculate(root, res, root->val);
        return res % MOD;
    }
private:
    const int MOD = 1000000007;
    void dfs(TreeNode* node) {
        if (node == nullptr) return;        
        if (node->left == node->right) return;
        
        dfs(node->left);
        dfs(node->right);
        
        if (node->left != nullptr) node->val += node->left->val;
        if (node->right != nullptr) node->val += node->right->val;
    }
    
    void calculate(TreeNode* node, long long& res, const int& total) {
        if (node == nullptr) return;        
        if (node->left == node->right) return;
        
        if (node->left) {
            long long one = node->left->val;
            long long another = total - one;
            res = max(res, one * another);
        }
        if (node->right) {
            long long one = node->right->val;
            long long another = total - one;
            res = max(res, one * another);
        }
        
        calculate(node->left, res, total);
        calculate(node->right, res, total);
    }
};
```

