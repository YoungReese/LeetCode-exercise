https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-transaction-fee/

```c++
// buy[i]  => 表示第 i 天持有股票时的最大收益 
// sell[i] => 表示第 i 天不持有股票时的最大收益
class Solution {
public:
    int maxProfit(vector<int>& prices, int fee) {
        int n = prices.size();
        if (n < 2) return 0;
        vector<int> buy(n + 1, INT_MIN / 2);
        vector<int> sell(n + 1, 0);
        for (int i = 1; i <= n; ++i) {
            buy[i] = max(buy[i - 1], sell[i - 1] - prices[i - 1]);
            sell[i] = max(sell[i - 1], buy[i - 1] + prices[i - 1] - fee);
        }
        return sell[n];
    }
};
```



