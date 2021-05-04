https://leetcode.com/problems/implement-trie-prefix-tree/

```c++
class Trie {
private:
    class TrieNode {
    public:
        bool isWord;
        vector<TrieNode*> children;
        TrieNode() {
            isWord = false;
            children = vector<TrieNode*>(26, nullptr);
        }
    };
private:
    TrieNode* root;
public:
    /** Initialize your data structure here. */
    Trie() {
        root = new TrieNode();
    }
    /** Inserts a word into the trie. */
    void insert(string word) {
        TrieNode* node = root;
        for (char c : word) {
            if (!node->children[c - 'a']) node->children[c - 'a'] = new TrieNode();
            node = node->children[c - 'a'];
        }
        node->isWord = true;
    }
    /** Returns if the word is in the trie. */
    bool search(string word) {
        TrieNode* node = root;
        for (char c : word) {
            if (node->children[c - 'a']) node = node->children[c - 'a'];
            else return false;
        }
        return node->isWord;
    }
    /** Returns if there is any word in the trie that starts with the given prefix. */
    bool startsWith(string prefix) {
        TrieNode* node = root;
        for (char c : prefix) {
            if (node->children[c - 'a']) node = node->children[c - 'a'];
            else return false;
        }
        return true;
    }
};

/**
 * Your Trie object will be instantiated and called as such:
 * Trie* obj = new Trie();
 * obj->insert(word);
 * bool param_2 = obj->search(word);
 * bool param_3 = obj->startsWith(prefix);
 */
```



```java
class Trie {
    private TrieNode root;
    /** Initialize your data structure here. */
    public Trie() {
        root = new TrieNode();
    }
    /** Inserts a word into the trie. */
    public void insert(String word) {
        TrieNode node = root;
        char[] c = word.toCharArray();
        for (int i = 0, n = word.length(); i < n; ++i) {
            if (node.children[c[i] - 'a'] == null) node.children[c[i] - 'a'] = new TrieNode();
            node = node.children[c[i] - 'a'];
        }
        node.isWord = true;
    }
    /** Returns if the word is in the trie. */
    public boolean search(String word) {
        TrieNode node = root;
        char[] c = word.toCharArray();
        for (int i = 0, n = word.length(); i < n; ++i) {
            if (node.children[c[i] - 'a'] == null) return false;
            node = node.children[c[i] - 'a'];
        }
        return node.isWord;
    }
    /** Returns if there is any word in the trie that starts with the given prefix. */
    public boolean startsWith(String prefix) {
        TrieNode node = root;
        char[] c = prefix.toCharArray();
        for (int i = 0, n = prefix.length(); i < n; ++i) {
            if (node.children[c[i] - 'a'] == null) return false;
            node = node.children[c[i] - 'a'];
        }
        return true;
    }
    
    private static class TrieNode {
        boolean isWord;
        TrieNode[] children;
        public TrieNode() {
            isWord = false;
            children = new TrieNode[26];
        }
    }
}

/**
 * Your Trie object will be instantiated and called as such:
 * Trie obj = new Trie();
 * obj.insert(word);
 * boolean param_2 = obj.search(word);
 * boolean param_3 = obj.startsWith(prefix);
 */
```

