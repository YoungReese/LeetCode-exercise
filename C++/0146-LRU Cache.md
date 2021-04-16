https://leetcode.com/problems/lru-cache/

```c++
class LRUCache {
public:
    LRUCache(int capacity) : capacity(capacity) {}

    int get(int key) {
        if (um.count(key) == 0) return -1;
        int value = um[key]->value;
        put(key, value);
        return value;
    }

    void put(int key, int value) {
        if (um.count(key) != 0) {
            cache.remove(um[key]);
        } else if (um.size() == capacity) {
            int lastKey = cache.removeLast();
            um.erase(lastKey);
        }
        Node* node = new Node(key, value);
        cache.addFirst(node);
        um[key] = node;
    }

 private:
    struct Node {
        int key, value;
        Node* next;
        Node* prev;
        Node(int k, int v) : key(k), value(v), next(nullptr), prev(nullptr) {}
    };

    class DoubleLinkedList {
    private:
        Node* head = nullptr;
        Node* tail = nullptr;

    public:
        void addFirst(Node* node) {
            if (head == nullptr) {
                head = tail = node;
            } else {
                node->next = head;
                head->prev = node;
                head = node;
            }
        }

        int removeLast() {
            int key = tail->key; // 返回 key，不返回 tail 是因为 c++ 在 remove 中会把 node 使用 delete 释放
            remove(tail);        // 因此调用 removeLast 的地方，使用 node->key 会报空指针异常
            return key;
        }

        void remove(Node* node) {
            if (node == head && node == tail) {
                head = tail = nullptr;
            } else if (node == head) {
                head = head->next;
                node->next->prev = nullptr;
                node->next = nullptr;
            } else if (node == tail) {
                tail = tail->prev;
                node->prev->next = nullptr;
                node->prev = nullptr;
            } else {
                node->prev->next = node->next;
                node->next->prev = node->prev;
                node->prev = nullptr;
                node->next = nullptr;
            }
            delete node;
            node = nullptr;
        }
    };

private:
    int capacity;
    DoubleLinkedList cache;
    unordered_map<int, Node*> um;
};

/**
 * Your LRUCache object will be instantiated and called as such:
 * LRUCache* obj = new LRUCache(capacity);
 * int param_1 = obj->get(key);
 * obj->put(key,value);
 */
```



```java
public class LRUCache {

    private HashMap<Integer, Node> m; // key 映射到 Node(key, val)
    private DoubleLinkedList cache;   // 双向链表
    private int capacity;             // 容量

    public LRUCache(int capacity) {
        this.capacity = capacity;
        m = new HashMap<>();
        cache = new DoubleLinkedList();
    }

    public int get(int key) {           // O(1)
        if (!m.containsKey(key)) return -1;
        int value = m.get(key).value;
        put(key, value);
        return value;
    }

    public void put(int key, int val) { // O(1)
        if (m.containsKey(key)) {
            cache.remove(m.get(key));
        } else if (cache.size() == capacity) {
            Node last = cache.removeLast();
            m.remove(last.key);
        }
        Node node = new Node(key, val);
        cache.addFirst(node);
        m.put(key, node);
    }

    // 内部双向链表类
    private static class DoubleLinkedList {

        private Node head, tail;
        private int size;

        public void addFirst(Node node) {
            if (head == null) {
                head = tail = node;
            } else {
                head.prev = node;
                node.next = head;
                head = node;
            }
            size++;
        }

        public void remove(Node node) {
            if (node == head && node == tail) {
                head = tail = null;
            } else if (node == tail) {
                tail = node.prev;
                node.prev.next = null;
                node.prev = null;
            }  else if (node == head) {
                head = node.next;
                node.next.prev = null;
                node.next = null;
            } else {
                node.prev.next = node.next;
                node.next.prev = node.prev;
                node.next = null;
                node.prev = null;
            }
            size--;
        }

        public Node removeLast() {
            Node node = tail;
            remove(tail);
            return node;
        }

        public int size() {
            return size;
        }
    }

    // 内部节点类
    private static class Node {
        public int key, value;
        public Node next, prev;
        public Node (int k, int v) {
            this.key = k;
            this.value = v;
        }
    }
}

/**
 * Your LRUCache object will be instantiated and called as such:
 * LRUCache obj = new LRUCache(capacity);
 * int param_1 = obj.get(key);
 * obj.put(key,value);
 */
```





