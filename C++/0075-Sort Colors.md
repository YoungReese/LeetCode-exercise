https://leetcode.com/problems/sort-colors/

```c++
class Solution {
public:
    void sortColors(vector<int>& nums) {
        int left = 0, right = nums.size() - 1;
        for (int i = 0; i <= right; ++i) {
            if (nums[i] == 0) swap(nums[i], nums[left++]);
            else if (nums[i] == 2) swap(nums[i--], nums[right--]); // 后面换过来的 num 需要在确认一下是否为 0
        }
    }
};
```

