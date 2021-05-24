https://leetcode.com/problems/max-points-on-a-line/

```c++
// All the points are unique.
class Solution {
public:
    int maxPoints(vector<vector<int>>& points) {
        unordered_map<double, int> hash;                // <斜率，个数>
        int res = 0;
        for (int i = 0, n = points.size(); i < n; ++i) {
            int same = 1, sameX = 1;
            for (int j = i + 1; j < n; ++j) {
                if (points[j][0] == points[i][0]) {     // 斜率不存在，横坐标相同 
                    ++sameX;                        
                    // if (points[j][1] == points[i][1]) { // 纵坐标也相同 => 重复的点（针对重复点的解法）
                    //     ++same;
                    // }
                } else {
                    double k = (points[j][1] - points[i][1]) * 1.0 / (points[j][0] - points[i][0]);
                    ++hash[k];
                }
            }
            res = max(res, sameX);
            for (auto& e : hash) {
                res = max(res, same + e.second); // 本题 same 可以直接使用 1
            }
            hash.clear();
        }
        return res;
    }
};
```

