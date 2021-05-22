https://leetcode.com/problems/max-chunks-to-make-sorted/

```c++
class Solution {
public:
    int maxChunksToSorted(vector<int>& arr) {
        int res = 0;
        int maxNum = 0;
        for (int i = 0, n = arr.size(); i < n; ++i) {
            maxNum = max(maxNum, arr[i]);
            if (maxNum == i) ++res;
        }
        return res;
    }
};
```


