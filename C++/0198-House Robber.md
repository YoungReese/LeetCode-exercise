https://leetcode.com/problems/house-robber/

```c++
class Solution {
public:
    int rob(vector<int>& nums) {
        if (nums.size() == 1) return nums[0]; 
        int n = nums.size();
        vector<int> dp(n + 1, 0);
        dp[1] = nums[0];
        for (int i = 2; i <= n; ++i) {
            dp[i] = max(dp[i - 1], dp[i - 2] + nums[i - 1]);
        }
        return dp[n];
    }
};
```



```c++
class Solution {
public:
    int rob(vector<int>& nums) {
        if (nums.size() == 1) return nums[0]; 
        int pre0 = 0, pre1 = nums[0], money;
        for (int i = 2, n = nums.size(); i <= n; ++i) {
            money = max(pre1, pre0 + nums[i - 1]);
            pre0 = pre1;
            pre1 = money;
        }
        return money;
    }
};
```

