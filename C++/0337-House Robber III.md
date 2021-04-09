https://leetcode.com/problems/house-robber-iii/

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
    int rob(TreeNode* root) {
        int lm = 0, rm = 0;
        return dfs(root, lm, rm);
    }
private:
    int dfs(TreeNode* node, int& lm, int& rm) {
        if (node == nullptr) return 0;
        int llm = 0, lrm = 0, rlm = 0, rrm = 0;
        lm = dfs(node->left, llm, lrm);
        rm = dfs(node->right, rlm, rrm);
        return max(lm + rm, llm + lrm + rlm + rrm + node->val);
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
// 拿root(第0层)为例,如果取第0层的节点,则第1层的节点不能取;
// 如果不取第0层的节点,则第1层的节点可取可不取;
// 这样我们需要记录下每个节点取与不取时能够获取的最大钱数;
// 通过DFS遍历二叉树，最后取root节点返回的两个数值中大的就可以了.
class Solution {
private:
    vector<int> dfs(TreeNode* root){
        // ret[0]: 偷(取)该节点  
        // ret[1]: 不偷(取)该节点
        vector<int> ret(2, 0);
        if(root == nullptr) return ret;
        
        vector<int> lRet = dfs(root->left);
        vector<int> rRet = dfs(root->right);
        
        ret[0] = lRet[1] + rRet[1] + root->val;
        ret[1] = max(lRet[0], lRet[1]) + max(rRet[0], rRet[1]);
        return ret;
    }
public:
    int rob(TreeNode* root) {
        vector<int> ret = dfs(root);
        return max(ret[0], ret[1]);
    }
};
```

