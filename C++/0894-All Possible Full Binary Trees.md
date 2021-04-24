https://leetcode.com/problems/all-possible-full-binary-trees/

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
// 终极版
class Solution {
public:
    vector<TreeNode*> allPossibleFBT(int n) {
        if ((n & 1) == 0) return {};
        unordered_map<int, vector<TreeNode*>> memo;
        memo[1] = vector<TreeNode*>{new TreeNode()};
        return helper(n, memo);
    }
private:
    vector<TreeNode*> helper(int n, unordered_map<int, vector<TreeNode*>>& memo) {
        if (memo.find(n) != memo.end()) return memo[n];
        
        vector<TreeNode*> res;
        for (int i = 1; i < n; i += 2) {
            for (TreeNode* leftNode : helper(i, memo)) {
                for (TreeNode* rightNode : helper(n - i - 1, memo)) {
                    TreeNode* node = new TreeNode();
                    node->left = leftNode;
                    node->right = rightNode;
                    res.push_back(node);
                }
            }
        }
        
        memo[n] = res;
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
// 第二版
class Solution {
public:
    vector<TreeNode*> allPossibleFBT(int n) {
        if ((n & 1) == 0) return {};
        unordered_map<int, vector<TreeNode*>> memo;
        return helper(1, n, memo);
    }
private:
    vector<TreeNode*> helper(int start, int end, unordered_map<int, vector<TreeNode*>>& memo) {
        if (memo.find(end - start) != memo.end()) return memo[end - start];
        if (start == end) return {new TreeNode()};
        
        vector<TreeNode*> res;
        for (int i = start + 1; i < end; i += 2) {
            for (TreeNode* leftNode : helper(start, i - 1, memo)) {
                for (TreeNode* rightNode : helper(i + 1, end, memo)) {
                    TreeNode* node = new TreeNode();
                    node->left = leftNode;
                    node->right = rightNode;
                    res.push_back(node);
                }
            }
        }
        
        memo[end - start] = res;
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
// 第一版
class Solution {
public:
    vector<TreeNode*> allPossibleFBT(int n) {
        if ((n & 1) == 0) return {};
        return helper(1, n);
    }
private:
    vector<TreeNode*> helper(int start, int end) {
        if (start == end) return {new TreeNode()};

        vector<TreeNode*> res;
        for (int i = start + 1; i < end; i += 2) {
            for (TreeNode* leftNode : helper(start, i - 1)) {
                for (TreeNode* rightNode : helper(i + 1, end)) {
                    TreeNode* node = new TreeNode();
                    node->left = leftNode;
                    node->right = rightNode;
                    res.push_back(node);
                }
            }
        }
        
        return res;
    }
};
```
