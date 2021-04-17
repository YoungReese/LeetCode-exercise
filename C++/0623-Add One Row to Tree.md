https://leetcode.com/problems/add-one-row-to-tree/

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
    TreeNode* addOneRow(TreeNode* root, int val, int depth) {     
        if (depth == 1) {
            TreeNode* newRoot = new TreeNode(val);
            newRoot->left = root;
            return newRoot;
        }
        
        queue<TreeNode*> q;
        q.push(root);
        while (!q.empty()) {
            depth--;
            TreeNode* node;
            for (int i = 0, n = q.size(); i < n; i++) {
                node = q.front(); q.pop();
                if (depth == 1) {
                    TreeNode* newLeftNode = new TreeNode(val);
                    TreeNode* newRightNode = new TreeNode(val);
                    
                    newLeftNode->left = node->left;
                    newRightNode->right = node->right;
                    
                    node->left = newLeftNode;
                    node->right = newRightNode;
                } else {
                    if (node->left) q.push(node->left);
                    if (node->right) q.push(node->right);
                }
            }
            if (depth == 1) break;
        }
        return root;
    }
};
```


