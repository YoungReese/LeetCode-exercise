https://leetcode.com/problems/longest-consecutive-sequence/

```c++
// 从当前数字向两边扩展
class Solution {
public:
    int longestConsecutive(vector<int>& nums) {
        unordered_set<int> us;
        for (int& num : nums) us.insert(num);
        int res = 0, prev, next;
        while (!us.empty()) {
            int num = *(us.begin());
            us.erase(num);
            prev = num - 1; next = num + 1;
            while (us.find(prev) != us.end()) {
                us.erase(prev--);
            }
            while (us.find(next) != us.end()) {
                us.erase(next++);
            }
            res = max(res, next - prev - 1);
        }
        return res;
    }
};
```

