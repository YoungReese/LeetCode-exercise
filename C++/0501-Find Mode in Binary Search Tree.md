https://leetcode.com/problems/find-mode-in-binary-search-tree/

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
    vector<int> findMode(TreeNode* root) {
        if (root == nullptr) return {};
        int preVal = INT_MIN;
        int count = 0;
        int maxCount = 0;
        vector<int> res;
        inorder(root, preVal, count, maxCount, res);
        return res;
    }
private:
    void inorder(TreeNode* node, int& preVal, int& count, int& maxCount, vector<int>& res) {
        if (node == nullptr) return;
        inorder(node->left, preVal, count, maxCount, res);
        count = (node->val == preVal) ? count + 1 : 1;
        if (count > maxCount) {
            maxCount = count;
            res.clear();
            res.push_back(node->val);
        } else if (count == maxCount) res.push_back(node->val);
        preVal = node->val;
        inorder(node->right, preVal, count, maxCount, res); 
    }
};
```


