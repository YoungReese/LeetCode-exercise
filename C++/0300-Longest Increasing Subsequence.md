https://leetcode.com/problems/longest-increasing-subsequence/

```c++
// dp[i]：[0, i) 以 nums[i - 1] 结尾的数组中的最长子序列个数
// O(n^2) O(n)
class Solution {
public:
    int lengthOfLIS(vector<int>& nums) {
        int n = nums.size();
        if (n == 1) return 1;
        vector<int> dp(n, 1);
        int res = 1;
        for (int i = 1; i < n; ++i) {
            for (int j = i - 1; j >= 0; --j) {
                if (nums[i] > nums[j]) dp[i] = max(dp[i], dp[j] + 1);
            }
            res = max(res, dp[i]);
        }
        return res;
    }
};
```



```c++
// 维护一个递增序列的 dp 数组，里面数字个数就是最长的子序列个数（注意：但是不一定就是子序列对应的值）
// Return iterator to lower bound: an iterator pointing to the first element 
// in the range [first,last) which does not compare less than val.
// O(n logn)  O(n)
class Solution {
public:
    int lengthOfLIS(vector<int>& nums) {
        int n = nums.size();
        if (n == 1) return 1;
        vector<int> dp;
        dp.push_back(nums[0]);
        for (int i = 1; i < n; ++i) {
            if (nums[i] > dp.back()) dp.push_back(nums[i]);
            else {
                auto it = lower_bound(dp.begin(), dp.end(), nums[i]);
                *it = nums[i];
            }
        }
        return dp.size();
    }
};
```

