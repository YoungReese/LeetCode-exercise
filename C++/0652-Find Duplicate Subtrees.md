https://leetcode.com/problems/find-duplicate-subtrees/

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
    vector<TreeNode*> findDuplicateSubtrees(TreeNode* root) {
        unordered_map<string, int> um;
        vector<TreeNode*> res;
        decode(root, um, res);
        return res;
    }
private:
    string decode(TreeNode* node, unordered_map<string, int>& um, vector<TreeNode*>& res) {
        if (node == nullptr) return "#";
        string serial = to_string(node->val) + ","
            + decode(node->left, um, res) + ","
            + decode(node->right, um, res);
        if (++um[serial] == 2) res.push_back(node);
        return serial;
    }
};
```



```c++
// 这位直接使用hash的方法确实很快，也能通过，但是冲突了就会造成程序失败
// 可能数据量较小，选择的方法不会冲突
// 不推荐这种解答
class Solution {
    unordered_map<int, int> H;
    vector<TreeNode*> R;
public:
    vector<TreeNode*> findDuplicateSubtrees(TreeNode* r) {
        T(r);
        return R;
    }
    unsigned int T(TreeNode* r) {
        if (r == nullptr) return 123400;
        unsigned int hash = 0;
        hash = hash * 127 + T(r->left);
        hash = hash * 127 + T(r->right);
        hash = hash * 127 + r->val;
        hash = hash ^ (hash >> 10);
        if (++H[hash] == 2) R.push_back(r);
        return hash;
    }
};
```

