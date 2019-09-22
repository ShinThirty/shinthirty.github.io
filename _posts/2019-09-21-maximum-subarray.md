---
layout: post
title:  "LeetCode 53: Maximum Subarray"
date:   2019-09-21
categories: [note]
tags:   [leetcode, dynamic programming]
---
<script src='https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.5/MathJax.js?config=TeX-MML-AM_CHTML' async></script>

## Problem

Given an integer array `nums`, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.

Example:

```text
Input: [-2,1,-3,4,-1,2,1,-5,4],
Output: 6
Explanation: [4,-1,2,1] has the largest sum = 6.
```

## Solution

Set function $$f(n)$$ to be the largest sum of subarrays ending at index `n`,
then we have

$$
f(n) =
  \begin{cases}
    nums[0], &\quad n = 0 \\
    nums[n], &\quad f(n-1) \le 0 \\
    nums[n] + f(n-1), &\quad f(n-1) > 0 \\
  \end{cases}
$$

Obviously, we can calcuate $$f(n)$$ in $$O(n)$$ time. Once we have $$f(n)$$ for all `n` from `0` to `len(nums)-1`, we get the maximum sum of all subarrays.

Notice that we need only a single variable to store value $$f(n-1)$$ to calculate $$f(n)$$ in each iteration, so the space complextiy is $$O(1)$$.

## Code

```python
class Solution(object):
    def maxSubArray(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        prev = None
        res = None

        for i in range(len(nums)):
            if prev is None or prev < 0:
                prev = nums[i]
            else:
                prev += nums[i]

            if res is None or res < prev:
                res = prev

        return res
```
