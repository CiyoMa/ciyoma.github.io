---
layout: post
category: Leetcode
tags: [Leetcode, Binary Tree]
---
### Requirement:
Given a binary tree, find its maximum depth.

The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.

### Analysis:
Maximum depth (MD) from a not None node n is the larger depth of two maximum depth from the left and right subtrees plus one.

if n is None: MD(n) = 0

else: MD(n) = max(MD(n.left), MD(n.right))


### Code:
{% highlight python %}

# Definition for a  binary tree node
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    # @param root, a tree node
    # @return an integer
    def maxDepth(self, root):
        if not root:
            return 0
        return max(self.maxDepth(root.left), self.maxDepth(root.right)) + 1
 
{% endhighlight %}