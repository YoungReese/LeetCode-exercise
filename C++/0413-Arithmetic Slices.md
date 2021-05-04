https://leetcode.com/problems/arithmetic-slices/

```c++
// dp[i]：定义为以 nums[i] 结尾而增加的等差数列个数
// 因为等差数列可以在任意一个位置终结，所以最后求和即可
// A subarray is a contiguous subsequence of the array.
class Solution {
public:
    int numberOfArithmeticSlices(vector<int>& nums) {
        if (nums.size() < 3) return 0;
        int n = nums.size();
        vector<int> dp(n, 0);
        for (int i = 2; i < n; i++) {
            if (nums[i] - nums[i - 1] == nums[i - 1] - nums[i - 2]) 
                dp[i] = dp[i - 1] + 1;
        }
        return accumulate(dp.begin(), dp.end(), 0);
    }
};
```

