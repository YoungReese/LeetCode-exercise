https://leetcode.com/problems/top-k-frequent-elements/

```c++
// 两次桶排序（You may return the answer in any order.）
class Solution {
public:
    vector<int> topKFrequent(vector<int>& nums, int k) {
        unordered_map<int, int> counts;
        int maxCount = 0;
        for (int& num : nums) maxCount = max(maxCount, ++counts[num]);
        
        vector<vector<int>> buckets(maxCount + 1); // 将结果建立桶
        for (auto& p : counts) buckets[p.second].push_back(p.first);
        
        vector<int> res;
        for (int i = maxCount; i > 0 && k > res.size(); --i) {
            for (int& num : buckets[i]) {
                res.push_back(num);
                if (res.size() == k) return res;
            }
        }
        
        return res;
    }
};
```



```c++
class Solution {
public:
    vector<int> topKFrequent(vector<int>& nums, int k) {
        priority_queue<pair<int, int>, vector<pair<int, int>>, greater<pair<int, int>>> pq; //小顶堆
        unordered_map<int, int> cnt;
        for (auto num : nums) cnt[num]++;
        for (auto kv : cnt) {
            pq.push({kv.second, kv.first});
            while (pq.size() > k) pq.pop();
        }
        vector<int> res;
        while (!pq.empty()) {
            res.push_back(pq.top().second);
            pq.pop();
        }
        return res;
    }
};
```

