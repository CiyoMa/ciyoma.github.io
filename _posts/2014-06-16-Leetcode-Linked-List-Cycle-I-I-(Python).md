---
layout: post
category: Leetcode
tags: [Leetcode, Linked List]
---
### Requirement:
Given a linked list, return the node where the cycle begins. If there is no cycle, return null.

Follow up:
Can you solve it without using extra space?

### Analysis:
By analysis in [Cycle I](/leetcode/2014/06/16/Leetcode-Linked-List-Cycle-I-\(Python\))

    Two pointers, 1 move 1 node per time, another move 2 nodes per time. 

    If no cycle: The fast pointer will reach the tail first

    If it has cycle: the fast pointer will eventually meet the slow pointer again.

How to find the beginning node of the cycle?

Say the given linked list has a cycle with loop-length k.
The distance from head to the begining of cycle is t. 
We know that once faster pointer get into cycle, the faster pointer will get 1 position closer to the slow one per time till they meet. And slow one will behind the faster one t position when it get into the cycle. So when they meet, they are at k-t position (since faster pointer can only chase the slow one and can not turn over to the other direction). So initialize a new pointer and make it walk from list head at 1 position per time, while the slow pointer is walking at the same pace. When they meet again, this node is the entrance of the cycle. 

### Code:
{% highlight python  linenos anchorlinenos %}
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    # @param head, a ListNode
    # @return a list node
    def detectCycle(self, head):
        if head is None:
            return None
        p1 = head
        p2 = head.next
        while p2 != None and p1 != p2:
            p2 = p2.next
            if p2 == None:
                return None
            p1 = p1.next
            p2 = p2.next
        if p1 == p2:
            t = head
            p2 = p2.next
            while t != p2:
                t = t.next
                p2 = p2.next
            return t
        return None
{% endhighlight %}