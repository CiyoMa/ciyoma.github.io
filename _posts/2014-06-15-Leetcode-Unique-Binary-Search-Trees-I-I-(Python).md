---
layout: post
category: Leetcode
tags: [Leetcode, Binary Tree, Binary Search Tree, Dynamic Programming]
---
### Requirement:
Given n, generate all structurally unique BST's (binary search trees) that store values 1...n.

For example,

Given n = 3, there are a total of 5 unique BST's.

       1         3     3      2      1
        \       /     /      / \      \
         3     2     1      1   3      2
        /     /       \                 \
       2     1         2                 3

### Analysis:
This problem is a variant of [Unique BST](/leetcode/2014/06/15/Leetcode-Unique-Binary-Search-Trees-\(Python\)) and it also can be solved by dynamic programming (memorization).

Since the inorder traversal of any BST in the answer will be the same 1...n, we only need to record the start value and end value a BST need to cover. 

Suppose function buildTrees(start,end,memo) return the list of all distinct BSTs with value from start to end. Then the recursion can be expressed as:

For all t in [start, end], leftBranchSet = buildTrees(start, t-1, memo), rightBranchSet = buildTrees(t, end, memo), enumerate all combination of left and right subtrees, and output all these result.

Base case 1: start == end: return [TreeNode(start)]

Base case 2: start > end: return [None]

### Code:
{% highlight python  linenos anchorlinenos %}
# Definition for a  binary tree node
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    # @return a list of tree node
    def generateTrees(self, n):
        # @return a list of tree nodes, 
        # which are root nodes of binary search tree
        def buildTrees(start,end, memo={}):
            if start > end:
                return [None]
            if (start, end) in memo:
                return memo[(start, end)]
            if start == end:
                memo[(start, end)] = [TreeNode(start)]
                return memo[(start, end)]
            roots = []
            for i in range(start, end+1):
                leftCandidates = buildTrees(start, i-1, memo)
                rightCandidates = buildTrees(i+1, end, memo)
                for left in leftCandidates:
                    for right in rightCandidates:
                        root = TreeNode(i)
                        root.left = left
                        root.right = right
                        roots.append(root)
            memo[(start, end)] = roots
            return memo[(start, end)]
        return buildTrees(1,n)
{% endhighlight %}