https://leetcode.com/problems/count-complete-tree-nodes/

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
    int countNodes(TreeNode* root) {
        if (root == nullptr) return 0;
        return 1 + countNodes(root->left) + countNodes(root->right);
    }
};
```



**Follow up:** Traversing the tree to count the number of nodes in the tree is an easy solution but with `O(n)` complexity. Could you find a faster algorithm?

解法2参考资料：https://www.cnblogs.com/grandyang/p/4567827.html

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
    int countNodes(TreeNode* root) {
        if (root == nullptr) return 0;
        
        TreeNode* leftNode = root;
        TreeNode* rightNode = root;
        int leftHeight = 0;
        int rightHeight = 0;
        
        while (leftNode) {
            leftHeight++;
            leftNode = leftNode->left;
        }
        while (rightNode) {
            rightHeight++;
            rightNode = rightNode->right;
        }
        
        if (leftHeight == rightHeight) return pow(2, leftHeight) - 1;
        return 1 + countNodes(root->left) + countNodes(root->right);
    }
};
```

