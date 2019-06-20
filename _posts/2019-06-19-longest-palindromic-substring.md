---
layout: post
title:  "LeetCode 5: Longest Palindromic Substring"
date:   2019-06-19
categories: [note]
tags:   [leetcode, dynamic programming]
---
<script src='https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.5/latest.js?config=TeX-MML-AM_CHTML' async></script>

## Problem

* [Longest Palindromic Substring - LeetCode](https://leetcode.com/problems/longest-palindromic-substring/)

This is a famous problem regarding finding a maximum-length contiguous substring of a given string that is also a palindrome. For example, the longest palindromic substring of "bananas" is "anana". This problem is a perfect demonstration about how dynamic programming can save time compare to naive recursion.

## Algorithm

We want to check every single substring of the given string and determine whether it is palindromic or not. A string is palindromic when:

>1. Characters at boths sides are the same;
>2. The substring without the 2 side characters is palindromic.

There are two speical conditions when the length of the string is 1 or 2. A string is always palindromic when its length is 1. A string is palindromic when all characters are the same when its length is 2.

We can write this relationship as a simple math equation. Set $$i$$ and $$j$$ to be the starting and ending index of a substring within the given string. Set function $$f(i,j)$$ is $$True$$ when $$s[i:j-1]$$ is palindromic, $$False$$ otherwise. Then we have:

$$
f(i,j) =
  \begin{cases}
    True, &\quad i = j \\
    s[i] = s[j], &\quad j - i = 1 \\
    (s[i] = s[j]) \land f(i+1,j-1), &\quad j - i \ge 2 \\
  \end{cases}
$$

With the equation above, we can populate a 2D array containing all values of $$f(i,j) \text{ when } 0 \le i,j < n$$, while $$n$$ being the length of the input string. The populated 2D array should be like this for input string banana:

|   | b | a | n | a | n | a |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| b | T | F | F | F | F | F |
| a |   | T | F | T | F | T |
| n |   |   | T | F | T | F |
| a |   |   |   | T | F | T |
| n |   |   |   |   | T | F |
| a |   |   |   |   |   | T |

While we populating the 2D array, we can use two variables (```max_len``` and ```start```) to track the maximum length of palindromic substring and its starting index to find the final result.

Time complexity and space complexity of this algorithm are both $$O(n^2)$$ since we traverse through all combinations of $$(i,j)$$ and use a 2D array to store the results.

## Source Code

### Python

```python
class Solution(object):
    def longestPalindrome(self, s):
        """
        :type s: str
        :rtype: str
        """
        l = len(s)
        f = []
        for i in range(l):
            f.append([False] * l)

        for i in range(l):
            f[i][i] = True

        max_len = 1
        start = 0

        for i in range(l - 1):
            f[i][i+1] = (s[i] == s[i+1])
            if f[i][i+1] and max_len < 2:
                max_len = 2
                start = i

        for n in range(3, l+1):
            for i in range(l - n + 1):
                f[i][i+n-1] = (s[i] == s[i+n-1]) and f[i+1][i+n-2]
                if f[i][i+n-1] and max_len < n:
                    max_len = n
                    start = i

        return s[start:start+max_len]
```

## Furthur Reading

There is actually a more efficient algorithm called *Manacher's Algorithm* that can solve the problem in linear time. For furthur information, please check [this](https://www.hackerrank.com/topics/manachers-algorithm) article.
