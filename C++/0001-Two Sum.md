[1. Two Sum](https://leetcode.com/problems/two-sum/)

```c++
// O(n) O(n)
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        int n = nums.size();
        unordered_map<int, int> um;
        for (int i = 0; i < n; i++) {
            int need = target - nums[i];
            if (um.find(need) != um.end()) {
                return {um[need], i};
            }
            um[nums[i]] = i;
        }
        return {0, 0};
    }
};
```

