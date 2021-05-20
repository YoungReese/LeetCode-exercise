https://leetcode.com/problems/find-all-numbers-disappeared-in-an-array/

```c++
// 将出现过的数字对应角标位置的数字改为负数
// 然后遍历数组，大于 0 的表示该位置 + 1 的数字在数组中缺失
class Solution {
public:
    vector<int> findDisappearedNumbers(vector<int>& nums) {
        for (int i = 0, n = nums.size(); i < n; ++i) {
            int pos = abs(nums[i]) - 1;
            nums[pos] = nums[pos] > 0 ? -nums[pos] : nums[pos];
        }
        vector<int> res;
        for (int i = 0, n = nums.size(); i < n; ++i) {
            if (nums[i] > 0) res.push_back(i + 1);
        }
        return res;
    }
};
```


