https://leetcode.com/problems/first-missing-positive/

```c++
// table sort思想，将[1...x] (x <= n) 放到 [0...n - 1]
// 这样操作后，从左到右遍历的第一个数字不为 i + 1 （角标 + 1）即是第一个缺失的正数
// O(n)
class Solution {
public:
    int firstMissingPositive(vector<int>& nums) {
        int n = nums.size();
        for (int i = 0; i < n; i++) {
            while (nums[i] > 0 && nums[i] < n && nums[i] != nums[nums[i] - 1]) {
                swap(nums[i], nums[nums[i] - 1]);
            }
        }
        
        for (int i = 0; i < n; i++) {
            if (nums[i] != i + 1) return i + 1;
        }
        
        return n + 1;
    }
};
```



```c++
// O(nlog n)  O(1)
class Solution {
public:
    int firstMissingPositive(vector<int>& nums) {
        sort(nums.begin(), nums.end());

        int positive = 1;
        for (int i = 0, n = nums.size(); i < n; i++) {
            if (nums[i] <= 0) continue;
            if (nums[i] == positive) {
                while (i + 1 < n && nums[i + 1] == nums[i]) {
                    i++;
                }
                positive++;
            } else return positive;
        }
        
        return positive;
    }
};
```

