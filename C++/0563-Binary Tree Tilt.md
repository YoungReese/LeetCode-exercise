https://leetcode.com/problems/binary-tree-tilt/

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
    int findTilt(TreeNode* root) {
        int res = 0;
        calculateSum(root, res);
        return res;
    }
private:
    int calculateSum(TreeNode* node, int& res) { // postorder
        if (node == nullptr) return 0;
        int leftSum = calculateSum(node->left, res);
        int rightSum = calculateSum(node->right, res);
        res += (leftSum > rightSum ? (leftSum - rightSum) : (rightSum - leftSum));
        return leftSum + rightSum + node->val;
    }
};
```



