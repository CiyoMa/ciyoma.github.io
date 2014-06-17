---
layout: post
category: Leetcode
tags: [Leetcode, Linked List]
---
### Requirement:
Given a linked list, determine if it has a cycle in it.

Follow up:
Can you solve it without using extra space?

### Analysis:
Two pointers, 1 move 1 node per time, another move 2 nodes per time. 

If no cycle: The fast pointer will reach the tail first

If it has cycle: the fast pointer will eventually meet the slow pointer again.

### Code:
{% highlight python  linenos anchorlinenos %}
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    # @param head, a ListNode
    # @return a boolean
    def hasCycle(self, head):
    	if head is None:
    		return False
        p1 = head
        p2 = head.next
        while p2 != None and p1 != p2:
        	p2 = p2.next
        	if p2 == None:
        		return False
        	p1 = p1.next
        	p2 = p2.next
        if p1 == p2:
        	return True
        return False
{% endhighlight %}