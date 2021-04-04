https://leetcode.com/problems/path-sum-ii/

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
    vector<vector<int>> pathSum(TreeNode* root, int targetSum) {
        vector<int> ans;
        vector<vector<int>> res;
        dfs(root, targetSum, ans, res);
        return res;
    }
private:
    void dfs(TreeNode* node, int targetSum, vector<int>& ans, vector<vector<int>>& res) {
        if (node == nullptr) return;
        if (node->left == node->right) {
            if (node->val == targetSum) {
                ans.push_back(node->val);
                res.push_back(ans);
                ans.pop_back();
                return;
            }
        }
        ans.push_back(node->val);
        dfs(node->left, targetSum - node->val, ans, res);
        dfs(node->right, targetSum - node->val, ans, res);
        ans.pop_back();
    }
};
```

