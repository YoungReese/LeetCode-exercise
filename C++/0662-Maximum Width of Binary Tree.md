https://leetcode.com/problems/maximum-width-of-binary-tree/

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
    int widthOfBinaryTree(TreeNode* root) {
        unsigned res = 0;
        queue<pair<TreeNode*, unsigned>> q;
        q.push(make_pair(root, 0));
        while (!q.empty()) {
            if (q.size() == 1) q.front().second = 0; // optimized
            TreeNode* node;
            unsigned start = q.front().second, end = start;
            for (int i = 0, n = q.size(); i < n; i++) {
                node = q.front().first; 
                end = q.front().second; q.pop();
                if (node->left) q.push(make_pair(node->left, 2 * end + 1));
                if (node->right) q.push(make_pair(node->right, 2 * end + 2));
            }
            res = max(res, end - start + 1);
        }
        return res;
    }
};
```
