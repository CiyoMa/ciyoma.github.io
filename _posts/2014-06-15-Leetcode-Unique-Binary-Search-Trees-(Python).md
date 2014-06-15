---
layout: post
category: Leetcode
tags: [Leetcode, Binary Tree, Binary Search Tree, Dynamic Programming]
---
### Requirement:
Given n, how many structurally unique BST's (binary search trees) that store values 1...n?

For example,

Given n = 3, there are a total of 5 unique BST's.

       1         3     3      2      1
        \       /     /      / \      \
         3     2     1      1   3      2
        /     /       \                 \
       2     1         2                 3

### Analysis:

This problem can be solved by dynamic programming.

The value of root node can be selected from 1th to nth value in increasing ordering. Denote root node as t. 

So the remaining value can be classified into two groups: larger than n (group-size: n-t) or smaller than n (group-size: t-1). 

Therefore, the total number of distinct BST is 
$$ DP[n] = \sum_{all ~t \in [1, n]} DP[t-1]*DP[n-t]$$ 
$$ DP[0] = 1, ~ DP[1] = 1$$

### Code:
{% highlight python linenos=table %}
class Solution:
    # @return an integer
    def numTrees(self, n):
    	t = [1 for i in range(n+1)]
        for i in range(2,n+1):
        	temp = 0
        	for j in range(i):
        		temp += t[j] * t[i-j-1]
        	t[i] = temp
        return t[n]
{% endhighlight %}