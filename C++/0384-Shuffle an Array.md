https://leetcode.com/problems/shuffle-an-array/

```c++
// Fisher-Yates 洗牌算法
class Solution {
private:
    vector<int> origin, shuffled;
public:
    Solution(vector<int>& nums) : origin(nums), shuffled(nums) {}
    
    vector<int> reset() { return origin; }
    
    vector<int> shuffle() {
        int n = origin.size();
        // 可以使用反向或者正向洗牌，效果相同。 
        // 反向洗牌:
        for (int i = n - 1; i >= 0; --i) {
            swap(shuffled[i], shuffled[rand() % (i + 1)]);
        }
        // 正向洗牌:
        // for (int i = 0; i < n; ++i) {
        //     int pos = rand() % (n - i);
        //     swap(shuffled[i], shuffled[i + pos]);
        // }
        return shuffled;
    }
};

/**
 * Your Solution object will be instantiated and called as such:
 * Solution* obj = new Solution(nums);
 * vector<int> param_1 = obj->reset();
 * vector<int> param_2 = obj->shuffle();
 */
```



```c++
// 使用库函数
class Solution {
private:
    vector<int> origin, shuffled;
public:
    Solution(vector<int>& nums) : origin(nums), shuffled(nums) {}
    
    vector<int> reset() { return origin; }
    
    vector<int> shuffle() {
        random_shuffle(shuffled.begin(), shuffled.end());
        return shuffled;
    }
};

/**
 * Your Solution object will be instantiated and called as such:
 * Solution* obj = new Solution(nums);
 * vector<int> param_1 = obj->reset();
 * vector<int> param_2 = obj->shuffle();
 */
```

