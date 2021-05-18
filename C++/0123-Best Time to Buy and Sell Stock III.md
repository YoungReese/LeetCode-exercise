https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iii/

```c++
// 这里使用了降唯
// buy[i]  => 表示当天进行的是第 i 次交易持有股票时的收益
// sell[i] => 表示当天进行的是第 i 次交易不持有股票时的收益
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int n = prices.size();
        if (n < 2) return 0;
        vector<int> buy(3, INT_MIN);
        vector<int> sell(3, 0);
        for (int i = 1; i <= n; ++i) {
            buy[1] = max(buy[1], 0 - prices[i - 1]);
            sell[1] = max(sell[1], buy[1] + prices[i - 1]);
            buy[2] = max(buy[2], sell[1] - prices[i - 1]);
            sell[2] = max(sell[2], buy[2] + prices[i - 1]);       
        }
        return sell[2];
    }
};
```


