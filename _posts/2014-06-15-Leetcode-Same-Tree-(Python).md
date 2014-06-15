---
layout: post
category: Leetcode
tags: [Leetcode, Binary Tree]
---
### Requirement:
Given two binary trees, write a function to check if they are equal or not.

Two binary trees are considered equal if they are structurally identical and the nodes have the same value.

### Analysis:
Two trees are same, if and only if,

1. Current two nodes are the same. (Both none, or Both not None and have the same value)

2. The left/right subtrees of current two nodes are the same

### Code:
{% highlight python linenos=table %}

# Definition for a  binary tree node
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    # @param p, a tree node
    # @param q, a tree node
    # @return a boolean
    def isSameTree(self, p, q):
        if p and q and p.val == q.val:
            return self.isSameTree(p.left, q.left) and self.isSameTree(p.right, q.right)
        elif p is None and q is None:
            return True
        else:
            return False
{% endhighlight %}