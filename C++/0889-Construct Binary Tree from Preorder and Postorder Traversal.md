https://leetcode.com/problems/construct-binary-tree-from-preorder-and-postorder-traversal/

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
// 多个解，因为可以利用 pre 确定根，然后去 post 确定本次划分
// 也可以利用 post 确定根，然后去 pre 确定本次划分
class Solution { // pre: 根左右  post：左右根
public:
    TreeNode* constructFromPrePost(vector<int>& pre, vector<int>& post) {
        return constructTree(pre, 0, pre.size() - 1, post, 0, post.size() - 1);
    }
private:
    TreeNode* constructTree(vector<int>& pre, int preStart, int preEnd,
                            vector<int>& post, int postStart, int postEnd) {
        
        if (preStart > preEnd) return nullptr;
        if (preStart == preEnd) return new TreeNode(pre[preStart]);
        
        TreeNode* node = new TreeNode(pre[preStart]);
        int i = postStart;
        for (; i <= postEnd; i++) {
            if (post[i] == pre[preStart + 1]) break;
        }
        int cnt = i - postStart + 1;
        
        node->left = constructTree(pre, preStart + 1, preStart + cnt, post, postStart, i);
        node->right = constructTree(pre, preStart + cnt + 1, preEnd, post, i + 1, postEnd - 1);
        
        return node;
    }
};
```
