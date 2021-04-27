https://leetcode.com/problems/check-completeness-of-a-binary-tree/

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
    bool isCompleteTree(TreeNode* root) {
        queue<TreeNode*> q;
        q.push(root);
        // 用于记录本层的下一层前面出现左子树，没有右边子树的情况，或者左右子树均不存在
        // 如果在此基础上，本层的下一层或者下一层的下一层层序节点还有子节点，直接返回false
        bool flag = false; 
        while (!q.empty()) {
            TreeNode* node;
            for (int i = 0, n = q.size(); i < n; i++) {
                node = q.front(); q.pop();
                if (flag && (node->left || node->right)) return false;
                if (!node->left && node->right) return false;
                if (node->left == node->right || (node->left && !node->right)) flag = true;
                
                if (node->left) q.push(node->left);
                if (node->right) q.push(node->right); 
            }
        }
        return true;
    }
};
```

