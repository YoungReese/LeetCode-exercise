https://leetcode.com/problems/range-sum-query-immutable/

```c++
// sum[i] => the sum of num[0] to num[i - 1]
class NumArray {
public:
    NumArray(vector<int>& nums) : sum(vector<int>(nums.size() + 1, 0)) {
        int i = 1;
        for (int & num : nums) {
            sum[i] = sum[i - 1] + num;
            ++i;
        }
    }
    
    int sumRange(int left, int right) {
        return sum[right + 1] - sum[left];
    }
private:
    vector<int> sum;
};

/**
 * Your NumArray object will be instantiated and called as such:
 * NumArray* obj = new NumArray(nums);
 * int param_1 = obj->sumRange(left,right);
 */
```

