https://leetcode.com/problems/subarray-sum-equals-k/

```c++
// 从左到右不断遍历数组并记录前缀和出现的次数
class Solution {
public:
    int subarraySum(vector<int>& nums, int k) {
        int res = 0, sum = 0;
        unordered_map<int, int> um;
        um[0] = 1;
        for (int& num : nums) {
            sum += num;
            if (um.find(sum - k) != um.end()) {
                res += um[sum - k];
            }
            ++um[sum];
        }
        return res;
    }
};
```


