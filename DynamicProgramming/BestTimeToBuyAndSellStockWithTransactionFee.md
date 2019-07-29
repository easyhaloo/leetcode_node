Your are given an array of integers prices, for which the i-th element is the price of a given stock on day i; and a non-negative integer fee representing a transaction fee.

You may complete as many transactions as you like, but you need to pay the transaction fee for each transaction. You may not buy more than 1 share of a stock at a time (ie. you must sell the stock share before you buy again.)

Return the maximum profit you can make.

**Example 1:**

```verilog

Input: prices = [1, 3, 2, 8, 4, 9], fee = 2
Output: 8
Explanation: The maximum profit can be achieved by:
Buying at prices[0] = 1
Selling at prices[3] = 8
Buying at prices[4] = 4
Selling at prices[5] = 9
The total profit is ((8 - 1) - 2) + ((9 - 4) - 2) = 8.
```



来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-with-transaction-fee
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。



### 解析

> 这题是买卖股票系列中的又一题，一般这种题目都需要动态规划进行求解。
>
> 可以设置两个状态，第一个是当天不持有股票的最大收益(crash)，即当天不买或出售；第二个是当天持有股票的最大收益(hold)，即当天买入这支股票或者不买。
>
> 因此我们可以建立状态转移方程：
>
> Crash = Math.max(Crash,hold+prices[i] - fee)
>
> Hold =Math.max(hold, crash - prices[i])
>
> 在这里可以先求crash再求hold，可以减少临时变量的使用，因为hold是依赖crash的，这是因为题目的所要求的前置条件是买入之前必须先出售，当天卖当天买是亏损的，所以我们可以认定crash是一定大于hold的。



### 代码

```java
class Solution {
    public int maxProfit(int[] prices, int fee) {
         int crash = 0, hold = -prices[0];
        for (int i = 1; i < prices.length; i++) {
            crash = Math.max(crash, hold + prices[i] - fee);
            hold = Math.max(hold, crash - prices[i]);

        }
        return crash;
    }
}
```





### 参考

https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-with-transaction-fee/solution/yi-ge-fang-fa-tuan-mie-6-dao-gu-piao-wen-ti-by-l-2/