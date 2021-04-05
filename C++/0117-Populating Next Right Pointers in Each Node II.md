https://leetcode.com/problems/populating-next-right-pointers-in-each-node-ii/

```c++
/*
// Definition for a Node.
class Node {
public:
    int val;
    Node* left;
    Node* right;
    Node* next;

    Node() : val(0), left(NULL), right(NULL), next(NULL) {}

    Node(int _val) : val(_val), left(NULL), right(NULL), next(NULL) {}

    Node(int _val, Node* _left, Node* _right, Node* _next)
        : val(_val), left(_left), right(_right), next(_next) {}
};
*/
class Solution {
private:
    Node* getNextNode(Node* node) {
        while (node) {
            if (node->left) return node->left;
            if (node->right) return node->right;
            node = node->next;
        }
        return node;
    }
    
    void levelByLevelConnect(Node* node) {
        if (node == NULL) return;
        Node* tmp = node;
        while (tmp) {
            Node* r = tmp->right;
            if (tmp->left && tmp->right) tmp->left->next = tmp->right;
            else if (tmp->left) r = tmp->left;
            if (r) r->next = getNextNode(tmp->next);
            tmp = tmp->next;
        }
        levelByLevelConnect(getNextNode(node));
    }
public:
    Node* connect(Node* root) {
        levelByLevelConnect(root);
        return root;
    }
};
```



```c++
/*
// Definition for a Node.
class Node {
public:
    int val;
    Node* left;
    Node* right;
    Node* next;

    Node() : val(0), left(NULL), right(NULL), next(NULL) {}

    Node(int _val) : val(_val), left(NULL), right(NULL), next(NULL) {}

    Node(int _val, Node* _left, Node* _right, Node* _next)
        : val(_val), left(_left), right(_right), next(_next) {}
};
*/
class Solution {
private:
    Node* getNextNode(Node* node) {
        while (node) {
            if (node->left) return node->left;
            if (node->right) return node->right;
            node = node->next;
        }
        return node;
    }
public:
    Node* connect(Node* root) { // level by level to connect
        if (root == NULL) return root;
        Node* tmp = root;
        while (tmp) {
            Node* r = tmp->right;
            if (tmp->left && tmp->right) tmp->left->next = tmp->right;
            else if (tmp->left) r = tmp->left;
            if (r) r->next = getNextNode(tmp->next);
            tmp = tmp->next;
        }
        connect(getNextNode(root));
        return root;
    }
};
```

