---
layout: post
category: Leetcode
tags: [Leetcode]
---
### Requirement:
Reverse digits of an integer.

Example1: x = 123, return 321

Example2: x = -123, return -321

### Analysis:
initialize result = 0

Then, for every digits d from the least significant one to the most significant one, 

result *= 10, result += d

the for every digits d can be implemented as d = num % 10, num /= 10

return result with correct sign.

### Code:
{% highlight python linenos=table %}
class Solution:
    # @return an integer
    def reverse(self, x):
        result = 0
        flag = 1
        if x < 0:
            flag = -1
            x = abs(x)
        while x > 0:
            result *= 10
            result += x % 10
            x /= 10
        return flag * result
{% endhighlight %}