---
layout: post
category: Leetcode
tags: [Leetcode, Bit Magic]
---
### Requirement:
Given an array of integers, every element appears twice except for one. Find that single one.

Note:
Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?

### Analysis:
Number exclusive or itself yields 0. 0 exclusive or other number x will yield x itself. Bit magic is linear without using extra memory.

### Code:

    class Solution:
        # @param A, a list of integer
        # @return an integer
        def singleNumber(self, A):
            result = None
            for i in A:
                if result is None:
                    result = i
                else:
                    result ^= i
            return result