https://leetcode.com/problems/recover-a-tree-from-preorder-traversal/

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
// 分治递归
// If a node has only one child, that child is guaranteed to be the left child.
class Solution {
public:
    TreeNode* recoverFromPreorder(string S) {
        return helper(S, 0, S.size() - 1);
    }
private:
    TreeNode* helper(string& s, int left, int right) {
        // 保证 left 和 right 位置的字符非'-'，即指向的是数字字符
        if (left > right || left < 0 || right < 0) return nullptr;
        
        int i = left;
        int val = 0; 
        for (; i <= right; i++) {           // 获取该子树根结点的数字
            if (s[i] == '-') break;
            val = val * 10 + s[i] - '0';
        }
        
        TreeNode* node = new TreeNode(val); // 根据val创建该子树的根结点
        if (i > right) return node;
        
        int dash = 0;                       // 查找该子树的左右节点位置，需要先计算dash个数
        int left1 = -1, right1 = -1, left2 = -1, right2 = -1;
        for (; i <= right; i++) {
            if (s[i] == '-') dash++;
            else {
                left1 = i;    
                left2 = getLeft2(s, i + 1, right, dash);
                if (left2 > 0) {
                    right1 = left2 - dash;
                    right2 = right;
                } else {
                    right1 = right;
                }
                break;
            }
        }
        
        node->left = helper(s, left1, right1);
        node->right = helper(s, left2, right2);
        return node;
    }
    
    int getLeft2(const string& s, const int& index, const int& right, const int& dash) {
        for (int i = index; i <= right; i++) {
            if (s[i] != '-') continue;
            int curDash = 0;
            while (i < right && s[i] == '-') {
                curDash++;
                i++;
            }
            if (i <= right && curDash == dash) {
                return i;
            }
        }
        return -1; // 表示没找到
    }
};
```

