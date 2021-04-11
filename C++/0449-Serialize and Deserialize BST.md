https://leetcode.com/problems/serialize-and-deserialize-bst/

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
// 0 <= Node.val <= 10^4
class Codec {
public:
    // Encodes a tree to a single string.
    string serialize(TreeNode* root) {
        string s = "";
        encodeDfs(root, s); 
        return s;
    }

    // Decodes your encoded data to tree.
    TreeNode* deserialize(string data) {
        int index = 0;
        return decodeDfs(data, index);
    }
private:
    void encodeDfs(TreeNode* node, string& s) {
        if (node == nullptr) {
            s += "#";
            return;
        }
        s += to_string(node->val) + ",";
        encodeDfs(node->left, s);
        encodeDfs(node->right, s);   
    }
    TreeNode* decodeDfs(const string& s, int& index) {
        if (s[index] == '#') {
            index++;
            return nullptr;
        }
        int val = 0;
        while (s[index++] != ',') val = val * 10 + s[index - 1] - '0';
        
        TreeNode* node = new TreeNode(val);
        node->left = decodeDfs(s, index);
        node->right = decodeDfs(s, index);
        
        return node;
    }
};

// Your Codec object will be instantiated and called as such:
// Codec* ser = new Codec();
// Codec* deser = new Codec();
// string tree = ser->serialize(root);
// TreeNode* ans = deser->deserialize(tree);
// return ans;
```
