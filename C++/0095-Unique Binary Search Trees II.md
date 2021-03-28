https://leetcode.com/problems/unique-binary-search-trees-ii/

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
    vector<TreeNode*> generateTrees(int n) {
        if (n == 1) return {new TreeNode(1)};
        return generateBSTs(1, n);
    }
private:
    vector<TreeNode*> generateBSTs(const int& start, const int& end) {
        if (start > end) return {nullptr};
        vector<TreeNode*> res;
        for (int i = start; i <= end; i++) {
            vector<TreeNode*> leftNodes = generateBSTs(start, i - 1);
            vector<TreeNode*> rightNodes = generateBSTs(i + 1, end);
            for (TreeNode* leftNode : leftNodes) {
                for (TreeNode* rightNode : rightNodes) {
                    TreeNode* curNode = new TreeNode(i);
                    curNode->left = leftNode;
                    curNode->right = rightNode;
                    res.push_back(curNode);
                }
            }
        }
        return res;
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
// 记忆化减支
class Solution {
public:
    vector<TreeNode*> generateTrees(int n) {
        if (n == 1) return {new TreeNode(1)};
        vector<vector<vector<TreeNode*>>> memo(n, vector<vector<TreeNode*>>(n));
        return generateBSTs(1, n, memo);
    }
private:
    vector<TreeNode*> generateBSTs(const int& start, const int& end, vector<vector<vector<TreeNode*>>>& memo) {
        if (start > end) return {nullptr};
        if (memo[start - 1][end - 1].size() > 0) return memo[start - 1][end - 1];
        vector<TreeNode*> res;
        for (int i = start; i <= end; i++) {
            vector<TreeNode*> leftNodes = generateBSTs(start, i - 1, memo);
            vector<TreeNode*> rightNodes = generateBSTs(i + 1, end, memo);
            for (TreeNode* leftNode : leftNodes) {
                for (TreeNode* rightNode : rightNodes) {
                    TreeNode* curNode = new TreeNode(i);
                    curNode->left = leftNode;
                    curNode->right = rightNode;
                    res.push_back(curNode);
                }
            }
        }
        memo[start - 1][end - 1] = res;
        return res;
    }
};
```

