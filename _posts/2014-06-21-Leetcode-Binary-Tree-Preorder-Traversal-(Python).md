---
layout: post
category: Leetcode
tags: [Leetcode, Linked List]
---
### Requirement:
Given a binary tree, return the preorder traversal of its nodes' values.

For example:
Given binary tree {1,#,2,3},

       1
        \
         2
        /
       3

return [1,2,3].

Note: Recursive solution is trivial, could you do it iteratively?

### Analysis:

Recursive solution: super easy..

if root is not None, return [root.val] + recur(root.left) + recur(root.right),

else return []

Non-Recursive Solution: a little bit difficult.

*.  initialize stack with root node

1.  pop a not None node from stack, print it, put its right branch into the stack, then its left branch into the stack (so the left branch is always visited before the right branch).

2.  repeat till stack empty

### Code:

{% highlight python  linenos anchorlinenos %}
class Solution:
    # @param root, a tree node
    # @return a list of integers
    def preorderTraversal(self, root):
        result = []
        s = stack()
        s.push(root)
        while root and not s.isEmpty():
            cur = s.pop()
            result.append(cur.val)
            if cur.right:
                s.push(cur.right)
            if cur.left:
                s.push(cur.left)
        return result
{% endhighlight %}