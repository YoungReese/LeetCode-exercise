https://leetcode.com/problems/3sum-closest/

```c++
// O(n^2)  O(1)
class Solution {
public:
    int threeSumClosest(vector<int>& nums, int target) {
        if (nums.size() < 3) return 0;
        sort(nums.begin(), nums.end());
        int res = nums[0] + nums[1] + nums[2];
        for (int i = 0, n = nums.size(); i < n - 2; i++) {
            if (i > 0 && nums[i] == nums[i - 1]) continue;
            int left = i + 1, right = n - 1, curSum;
            while (left < right) {
                curSum = nums[i] + nums[left] + nums[right];
                if (curSum == target) return target;
                if (abs(res - target) > abs(curSum - target)) res = curSum;
                if (curSum < target) left++;
                else right--;
            }
        }
        return res;
    }
};
```

