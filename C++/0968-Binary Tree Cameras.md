https://leetcode.com/problems/binary-tree-cameras/

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
// Bottom to top（must）
class Solution {
public:
    int minCameraCover(TreeNode* root) {
        int res = 0;
        return dfs(root, res) == State::NONE ? ++res : res;
    }
private:
    enum class State { NONE = 0, COVERED = 1, CAMERA = 2 };
    State dfs(TreeNode* node, int& res) {
        
        if (node == nullptr) return State::COVERED; // currentNodeState should be
        
        State leftNodeState = dfs(node->left, res);
        State rightNodeState = dfs(node->right, res);
        
        if (leftNodeState == State::NONE || rightNodeState == State::NONE) {
            ++res;
            return State::CAMERA;  // currentNodeState should be
        }
        
        if (leftNodeState == State::CAMERA || rightNodeState == State::CAMERA) {
            return State::COVERED; // currentNodeState should be
        }
        
        return State::NONE;        // currentNodeState should be
    }
};
```

