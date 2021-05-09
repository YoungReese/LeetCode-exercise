https://leetcode.com/problems/partition-equal-subset-sum/

```c++
// optimized：背包问题中常规的空间压缩（推荐）
// O(n ^ target)
class Solution {
public:
    bool canPartition(vector<int>& nums) {
        int sum = accumulate(nums.begin(), nums.end(), 0), target = sum >> 1;
        if (sum & 1) return false;
        vector<bool> dp(target + 1, false);
        dp[0] = true;
        for (int num : nums) {
            // 使用此方法后，不使用的 dp[i] 会得到继承，所以可以限定 j >= num
            for (int j = target; j >= num; --j) {
                dp[j] = dp[j] || dp[j - num];
                if (j == target && dp[j]) return true;
            }
        }
        return dp[target];
    }
};
```



```c++
class Solution {
public:
    bool canPartition(vector<int>& nums) {
        if (nums.size() == 1) return false;
        int sum = accumulate(nums.begin(), nums.end(), 0);
        if (sum & 1) return false;
        int target = sum >> 1;
        int n = nums.size();
        vector<vector<bool>> dp(n + 1, vector<bool>(target + 1, false));
        for (int i = 0; i <= n; ++i) dp[i][0] = true;
        for (int i = 1; i <= n; ++i) {
            // j 必须从 1 开始，否则 dp[1][1] = true, 但是当 num[i - 1] > 1 时，dp[2][1] = false，没有被继承
            for (int j = 1; j <= target; ++j) { 
                dp[i][j] = dp[i - 1][j] || ((j >= nums[i - 1]) ? dp[i - 1][j - nums[i - 1]] : 0);
                if (j == target && dp[i][j]) return true;
            }
        }
        return dp[n][target];
    }
};
```



```c++
// 典型的背包问题，在 n 个物品中选出移动物品，填满 sum / 2 的背包
// F(n,c) 考虑将 n 个物品填满容量为c的背包
// F(i,c) = max(F(i, c), w[i] + F(i-1, c-w(i)))
class Solution {
public:
    bool canPartition(vector<int>& nums) {
        int sum = accumulate(nums.begin(), nums.end(), 0);
        if (sum & 1) return false;
        int target = sum >> 1;
        vector<int> dp(target + 1, 0);
        for(int j = 0; j <= target; ++j) dp[j] = (j >= nums[0]) ? nums[0] : 0;
        
        for(int i=1, n = nums.size(); i < n; ++i) {
            for(int j = target; j >= nums[i]; --j){
                dp[j] = max(dp[j], nums[i] + dp[j - nums[i]]);
                if(dp[j] == target) return true;
            }
        }
        return false;
    }
};
```



**新的思路，不建议使用，因为比较难理解**

>   **这道题还可以用 bitset 来做，bisets 的大小设为 10001，为啥呢，因为题目中说了数组的长度和每个数字的大小都不会超过 100，那么最大的和为 20000，那么一半就是 10000，前面再加上个0，就是 10001 了。初始化把最低位赋值为1，算出数组之和，然后遍历数字，对于遍历到的数字 num，把 bits 向左平移 num 位，然后再或上原来的 bits，这样所有的可能出现的和位置上都为1。举个例子来说吧，比如对于数组 [2,3] 来说，初始化 bits 为1，然后对于数字2，bits 变为 101，可以看出来 bits[2] 标记为了1，然后遍历到3，bits 变为了 101101，看到 bits[5]，bits[3]，bits[2] 都分别为1了，正好代表了`可能的和 2，3，5，`这样遍历完整个数组后，去看 bits[sum >> 1] 是否为1即可，参见代码如下：**

```c++
// O(n)
class Solution {
public:
    bool canPartition(vector<int>& nums) {
        bitset<10001> bits(1);
        int sum = accumulate(nums.begin(), nums.end(), 0);
        for (int num : nums) bits |= bits << num;
        return ((sum & 1) == 0) && bits[sum >> 1];
    }
};
```

