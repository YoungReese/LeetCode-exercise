https://leetcode.com/problems/design-skiplist/

```c++
class Skiplist {
private:
    const static int SKIPLIST_P = 5;
    const static int MAX_LEVEL = 16;
    int levelCount = 1;

private:
    class Node {
    public:
        int data = -1;
        int maxLevel = 0;
        vector<Node*> forward;
        Node() : forward(MAX_LEVEL) {}
        Node(int data, int maxLevel) : forward(MAX_LEVEL), data(data), maxLevel(maxLevel) {}
    };

private:
    Node* head;

public:
    Skiplist () {
        head = new Node();
    }

    bool search(int target) {
        Node* p = head;
        for (int i = levelCount - 1; i >= 0; i--) {
            while (p->forward[i] && p->forward[i]->data < target) {
                p = p->forward[i];
            }
        }
        if (p->forward[0] && p->forward[0]->data == target) return true;
        return false;
    }

    void add(int num) {
        int level = randomLevel();
        Node* newNode = new Node(num, level);

        vector<Node*> update(level);

        for (int i = 0; i < level; i++) {
            update[i] = head;
        }

        Node* p = head;
        for (int i = level - 1; i >= 0; i--) {
            while (p->forward[i] && p->forward[i]->data < num) {
                p = p->forward[i];
            }
            update[i] = p;
        }

        for (int i = 0; i < level; i++) {
            newNode->forward[i] = update[i]->forward[i];
            update[i]->forward[i] = newNode;
        }

        levelCount = level > levelCount ? level : levelCount;

    }

    bool erase(int num) {
        bool res = false;
        vector<Node*> update(levelCount);
        Node* p = head;
        for (int i = levelCount - 1; i >= 0; i--) {
            while (p->forward[i] && p->forward[i]->data < num) {
                p = p->forward[i];
            }
            update[i] = p;
        }
        if (p->forward[0] && p->forward[0]->data == num) {
            res = true;
            int level = p->forward[0]->maxLevel;
            Node* delNode = nullptr;
            for (int i = level - 1; i >= 0; i--) {
                if (update[i]->forward[i] && update[i]->forward[i]->data == num) {
                    delNode = update[i]->forward[i];
                    update[i]->forward[i] = update[i]->forward[i]->forward[i];
                }
            }
            delete delNode;
            delNode = nullptr;
        }
        while (levelCount > 1 && head->forward[levelCount - 1] == nullptr) {
            levelCount--;
        }
        return res;
    }

private:
    int randomLevel() {
        // srand((unsigned)time(NULL)); // 随机种子太耗时
        int level = 1;
        while (level < MAX_LEVEL && (rand() % 10) < SKIPLIST_P) level++;
        return level;
    }
}; 

/**
 * Your Skiplist object will be instantiated and called as such:
 * Skiplist* obj = new Skiplist();
 * bool param_1 = obj->search(target);
 * obj->add(num);
 * bool param_3 = obj->erase(num);
 */
```



```java
public class Skiplist {

    /**
     * 概率因子 0.5 表示每个节点有 1/2 机会被提升，可修改
     */
    private static final float SKIPLIST_P = 0.5f;

    /**
     * 限制最大层数，这里限制为16层，可修改
     */
    private final static int MAX_LEVEL = 16;

    /**
     * 记录当前跳表的层数，1 表示只有原链表，尚未建立索引
     */
    private int levelCount = 1;

    /**
     * 跳表带头节点，作用类似与 dummyHead or 哨兵
     */
    private Node head;

    public Skiplist() {
        head = new Node();
    }

    /**
     * 查找：从最高层的 head 开始想尾部查找，每当出现 data > value，降到下一层接力，直到原始链表层（1层，角标为0）
     */
    public boolean search(int target) {
        Node p = head;
        for (int i = levelCount - 1; i >= 0; i--) {
            while (p.forward[i] != null && p.forward[i].data < target) {
                p = p.forward[i];
            }
        }

        if (p.forward[0] != null && p.forward[0].data == target) return true;
        return false;
    }

    /**
     * 插入：1、先确定该节点可以最大提升到的层数
     *      2、创建新节点 newNode
     *      3、根据层数创建 update 数组（纵向，初始都指向 head）
     *      4、查找插入位置，更新后 update[i] 对应插入位置的前驱
     *      5、根据层数，从 0 层依次插入新的 newNode，更新 forward 数组
     */
    public void add(int num) {
        int level = randomLevel();
        Node newNode = new Node(num, level);

        Node[] update = new Node[level];
        for (int i = 0; i < level; i++) {
            update[i] = head;
        }

        Node p = head;
        for (int i = level - 1; i >=0; i--) {
            while (p.forward[i] != null && p.forward[i].data < num) {
                p = p.forward[i];
            }
            update[i] = p;
        }

        for (int i = 0; i < level; i++) {
            newNode.forward[i] = update[i].forward[i];
            update[i].forward[i] = newNode;
        }

        levelCount = level > levelCount ? level : levelCount;
    }

    /**
     * 删除：1、创建当前层数的 update 数组
     *      2、查找待删除节点的前驱节点 update[i]
     *      3、找到后按照层将前驱节点的下一跳改为下一跳的下一跳
     *      4、更新 levelCount
     */
    public boolean erase(int num) {
        Node[] update = new Node[levelCount];
        Node p = head;
        boolean res = false;
        for (int i = levelCount - 1; i >= 0; i--) {
            while (p.forward[i] != null && p.forward[i].data < num) {
                p = p.forward[i];
            }
            update[i] = p;
        }

        if (p.forward[0] != null && p.forward[0].data == num) {
            res = true;
            int level = p.forward[0].maxLevel;
            for (int i = level - 1; i >= 0; i--) {
                if (update[i].forward[i] != null && update[i].forward[i].data == num) {
                    update[i].forward[i] = update[i].forward[i].forward[i];
                }
            }
        }

        while (levelCount > 1 && head.forward[levelCount - 1] == null) {
            levelCount--;
        }

        return res;
    }

    /**
     * 因为这里SKIPLIST_P = 0.5f，所以
     *     1/2 的概率返回 1
     *     1/4 的概率返回 2
     *     1/8 的概率返回 3 ...
     */
    private int randomLevel() {
        int level = 1;
        while (level < MAX_LEVEL && Math.random() < SKIPLIST_P ) level++;
        return level;
    }

    private static class Node {
        private int data = -1;                            // 存储节点的数值
        private int maxLevel = 0;                         // 跳表当前节点的索引最大层数
        private Node[] forward = new Node[MAX_LEVEL];     // 当前节点所在层的横向下一跳
        Node() {}
        Node(int data, int maxLevel) {
            this.data = data;
            this.maxLevel = maxLevel;
        }
    }
}
/**
 * Your Skiplist object will be instantiated and called as such:
 * Skiplist* obj = new Skiplist();
 * bool param_1 = obj->search(target);
 * obj->add(num);
 * bool param_3 = obj->erase(num);
 */
```



