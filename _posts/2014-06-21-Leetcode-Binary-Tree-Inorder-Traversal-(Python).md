---
layout: post
category: Leetcode
tags: [Leetcode, Linked List]
---
### Requirement:
Given a binary tree, return the inorder traversal of its nodes' values.

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

if root is not None, return recur(root.left) + [root.val] + recur(root.right),

else return []

Non-Recursive Solution: a little bit difficult.

*.  initialize stack with root node

1.  pop a node from stack, go left, save every current node and its right branch into a stack util left is None.

2.  print this node

3.  pop stack util the popped node is the first node with right branch not None.

4.  repeat till stack empty


### Code:

{% highlight python  linenos anchorlinenos %}
# Definition for a  binary tree node
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None
class stack:
    def __init__(self):
        self.data = []
        
    def push(self, item):
        self.data.insert(0, item)
        
    def getTop(self):
        return self.data[0]
        
    def pop(self):
        result = self.data[0]
        self.data=self.data[1:]
        return result
        
    def isEmpty(self):
        return len(self.data) == 0
        
class Solution:
    # @param root, a tree node
    # @return a list of integers
    def inorderTraversal(self, root):
        result = []
        s = stack()
        s.push(root)
        while root and not s.isEmpty():
            node = s.pop()
            while node:
                if node.right:
                    s.push(node.right)
                s.push(node)
                node = node.left
                
            cur = s.pop()
            while not s.isEmpty() and not cur.right:
                result.append(cur.val)
                cur = s.pop()

            result.append(cur.val)
            # print result
            
        return result
{% endhighlight %}