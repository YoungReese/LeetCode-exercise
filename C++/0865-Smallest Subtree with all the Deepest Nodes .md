https://leetcode.com/problems/smallest-subtree-with-all-the-deepest-nodes/

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
    TreeNode* subtreeWithAllDeepest(TreeNode* root) {
        auto maxDepthPair = depth(root);
        return maxDepthPair.second;
    }
private:
    pair<int, TreeNode*> depth(TreeNode* node) {
        if (node == nullptr) return {0, nullptr};
        auto leftPair = depth(node->left);
        auto rightPair = depth(node->right);
        int d1 = leftPair.first, d2 = rightPair.first;
        return {1 + max(d1, d2), d1 == d2 ? node : (d1 > d2 ? leftPair.second : rightPair.second)};
    }
};
```



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
    TreeNode* subtreeWithAllDeepest(TreeNode* root) {
        unordered_map<TreeNode*, int> depth;
        int maxDepth = -1;
        dfs(root, 0, maxDepth, depth);
        return findDeepestSubtreeRoot(root, maxDepth, depth);   
    }
private:
    void dfs(TreeNode* node, int dist, int& maxDepth, 
             unordered_map<TreeNode*, int>& depth) {
        if (node == nullptr) return;
        maxDepth = max(maxDepth, dist);
        depth[node] = dist;
        dfs(node->left, dist + 1, maxDepth, depth);
        dfs(node->right, dist + 1, maxDepth, depth);
    }
    TreeNode* findDeepestSubtreeRoot(TreeNode* node, const int& maxDepth, 
                                     unordered_map<TreeNode*, int>& depth) {
        if (node == nullptr || depth[node] == maxDepth) return node;
        TreeNode* leftRoot = findDeepestSubtreeRoot(node->left, maxDepth, depth);
        TreeNode* rightRoot = findDeepestSubtreeRoot(node->right, maxDepth, depth);
        if (leftRoot && rightRoot) return node;
        if (leftRoot) return leftRoot;
        if (rightRoot) return rightRoot;
        return nullptr;
    }
};
```
