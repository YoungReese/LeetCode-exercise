https://leetcode.com/problems/random-pick-with-weight/

```c++
// 1 <= w[i] <= 10^5
// https://www.cplusplus.com/reference/numeric/partial_sum/?kw=partial_sum
// https://www.cplusplus.com/reference/algorithm/lower_bound/
class Solution {
private:
    vector<int> sums;
public:
    Solution(vector<int>& w) : sums(w) {
        partial_sum(sums.begin(), sums.end(), sums.begin());
    }
    
    int pickIndex() {
        int randomSum = (rand() % sums.back()) + 1;
        return lower_bound(sums.begin(), sums.end(), randomSum) - sums.begin();
    }
};

/**
 * Your Solution object will be instantiated and called as such:
 * Solution* obj = new Solution(w);
 * int param_1 = obj->pickIndex();
 */
```

