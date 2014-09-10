---
layout: post
category: Leetcode
tags: [Leetcode]
---
### Requirement:
Say you have an array for which the ith element is the price of a given stock on day i.

Design an algorithm to find the maximum profit. You may complete as many transactions as you like (ie, buy one and sell one share of the stock multiple times). However, you may not engage in multiple transactions at the same time (ie, you must sell the stock before you buy again).

### Analysis:
The sum of all increments is the maximum profit!

### Code:
{% highlight python  linenos anchorlinenos%}
class Solution:
    # @param prices, a list of integer
    # @return an integer
    def maxProfit(self, prices):
        delta = [0] + \
                [prices[i+1] - prices[i] for i in range(len(prices)-1)]
        return sum([i for i in delta if i >= 0])
{% endhighlight %}