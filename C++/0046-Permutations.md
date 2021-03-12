https://leetcode.com/problems/permutations/

```c++
// O(n!)
// 本题不需要完全实现完全有序的permutation，所以可以使用如下解法；
// 如果要实现完全有序的全排列，参考next_permutation实现。
class Solution {
public:
    vector<vector<int>> permute(vector<int>& nums) {
        int n = nums.size();
        if (n == 1) return {nums};
        vector<vector<int>> res;    
        generatePermute(nums, 0, res, n);
        return res;
    }
private:
    void generatePermute(vector<int>& nums, int startIndex, vector<vector<int>>& res, const int& n) {
        if (startIndex == n) {
            res.push_back(nums);
            return;
        }
        
        for (int i = startIndex; i < n; i++) {
            swap(nums[i], nums[startIndex]);
            generatePermute(nums, startIndex + 1, res, n);
            swap(nums[i], nums[startIndex]);
        }
    }
};
```

