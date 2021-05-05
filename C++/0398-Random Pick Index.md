https://leetcode.com/problems/random-pick-index/

```c++
// 水库抽烟算法
class Solution {
private:
    vector<int> nums;
public:
    Solution(vector<int>& nums) {
        this->nums = nums;
    }
    
    int pick(int target) {
        int res = 0;
        int count = 0;
        for (int i = 0, n = nums.size(); i < n; ++i) {
            if (nums[i] == target) {
                ++count;
                if ((rand() % count) == 0) res = i;
            }
        }
        return res;
    }
};

/**
 * Your Solution object will be instantiated and called as such:
 * Solution* obj = new Solution(nums);
 * int param_1 = obj->pick(target);
 */
```

