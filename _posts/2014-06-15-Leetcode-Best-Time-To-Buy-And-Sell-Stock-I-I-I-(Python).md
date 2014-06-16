---
layout: post
category: Leetcode
tags: [Leetcode, Dynamic Programming]
---
### Requirement:
Say you have an array for which the ith element is the price of a given stock on day i.

Design an algorithm to find the maximum profit. You may complete at most two transactions.

Note:
You may not engage in multiple transactions at the same time (ie, you must sell the stock before you buy again).

### Analysis:
First calculate maximum profit before each day, then calculate the maximum profit after each day, find the maximum of the sum. 

The first part is easy, just as the [variant I](/leetcode/2014/06/15/Leetcode-Best-Time-To-Buy-And-Sell-Stock-I-\(Python\)). For the second part, we have to find the maximum price no early than day i for all days, and calculate the difference between the current price and the maximum future price.

The maximum sum of current and future profit is the answer.

Therefore we get the maximum profit from all n days.

So the running time is O(n).

### Code:
{% highlight python linenos anchorlinenos %}
class Solution:
    # @param prices, a list of integer
    # @return an integer
    def maxProfit(self, prices):
    	if len(prices) <= 1:
    		return 0
        delta = [0] + [prices[i] - prices[i-1] for i in range(1, len(prices))]
        p = delta[:]
        for i in range(1, len(prices)):
            p[i] = max(p[i-1]+p[i], p[i])
        futureMax = [0 for i in range(len(prices))]
        futureBest = None
        for i in range(len(prices)-1, -1, -1):
            if futureBest is None or futureBest < prices[i]:
                futureBest = prices[i]
            futureMax[i] = max(futureBest,prices[i])
        bestEarnAfter = [0 for i in range(len(prices))]
        bestEarnAfter[len(prices)-1] = max(0,futureMax[len(prices)-1] - prices[len(prices)-1])
        for i in range(len(prices)-2, -1, -1):
        	bestEarnAfter[i] = max(bestEarnAfter[i+1],futureMax[i] - prices[i])
        return max([bestEarnAfter[i]+p[i] for i in range(len(prices))])
{% endhighlight %}