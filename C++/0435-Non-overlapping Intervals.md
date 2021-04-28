https://leetcode.com/problems/non-overlapping-intervals/

```c++
class Solution {
public:
    int eraseOverlapIntervals(vector<vector<int>>& intervals) {
        sort(intervals.begin(), intervals.end(), [&] (vector<int>& a, vector<int>& b) {
           return a[1] < b[1];
        });
        int res = 0, prev1 = intervals[0][1];
        for (int i = 1, n = intervals.size(); i < n; ++i) {
            if (intervals[i][0] < prev1) res++;
            else prev1 = intervals[i][1];
        }
        return res;
    }
};
```

