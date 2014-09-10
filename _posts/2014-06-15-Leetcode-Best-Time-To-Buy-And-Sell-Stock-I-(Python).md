---
layout: post
category: Leetcode
tags: [Leetcode, Dynamic Programming]
---
### Requirement:
Say you have an array for which the ith element is the price of a given stock on day i.

If you were only permitted to complete at most one transaction (ie, buy one and sell one share of the stock), design an algorithm to find the maximum profit.

### Analysis:
Solve it by Dynamic Programming!
The maximum profit at day i is denoted as p[i]. The choice at day i+1 is either to sell it that day or sell it after that day (keep the profit for future). So choose the better one.

Therefore, $$p[i] = max(p[i-1]+prices[i]-prices[i-1], prices[i]-prices[i-1]) $$
$$ p[0] = 0 $$

Then we get the maximum profit from all n days.

So the running time is O(n).

### Code:
{% highlight python linenos anchorlinenos %}
class Solution:
    # @param prices, a list of integer
    # @return an integer
    def maxProfit(self, prices):
    	delta = [0] + [prices[i+1] - prices[i] for i in range(len(prices)-1)]
        p = delta
        for i in range(1, len(p)):
        	p[i] = max(p[i-1]+p[i], p[i])
        return max(p)
{% endhighlight %}