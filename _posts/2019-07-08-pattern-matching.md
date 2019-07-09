---
layout: post
title:  "LeetCode 10: Regular Expression Matching and LeetCode 44: Wildcard Matching"
date:   2019-07-12
categories: [note]
tags:   [leetcode, dynamic programming]
---
<script src='https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.5/latest.js?config=TeX-MML-AM_CHTML' async></script>

## Overview

* [Regular Expression Matching](https://leetcode.com/problems/regular-expression-matching/)
* [Wildcard Matching](https://leetcode.com/problems/wildcard-matching/)

These two problems have similar structure and solution. For input string `s` and pattern `p`, the basic idea is:

1. Determine whether s[0] and p[0] matches or not;

2. Determine whether s[1:] and p[1:] matches or not recursively.

## Regular Expression Matching

For input string `s` and pattern `p`, we can define a match function $$isMatch(s, p)$$ as follows:

$$
isMatch(s,p) =
  \begin{cases}
    len(s) = 0, &\quad len(p) = 0 \\
    (p[0] = s[0] \lor p[0] = '.') \land isMatch(s[1:], p[1:]), &\quad len(p) = 1 \lor (len(p) > 1 \land p[1] \ne '*') \\
    ((p[0] = s[0] \lor p[0] = '.') \land isMatch(s[1:], p)) \lor isMatch(s, p[2:]), &\quad len(p) > 1 \land p[1] = '*' \\
  \end{cases}
$$

If we define a function $$f(i,j) = isMatch(s[i:], p[j:]), m = len(s), n = len(p)$$, then the above relationship can be rewritten as

$$
f(i,j) =
  \begin{cases}
    i = m, &\quad j = n \\
    (p[j] = s[i] \lor p[j] = '.') \land f(i+1,j+1), &\quad j = n-1 \lor (j < n-1 \land p[j+1] \ne '*') \\
    ((p[j] = s[i] \lor p[j] = '.') \land f(i+1,j)) \lor f(i,j+2), &\quad j < n-1 \land p[j+1] = '*' \\
  \end{cases}
$$

The result we are pursuing is $$f(0,0)$$. Since $$f(i,j)$$ can always be constructed with $$f(i+1,j+1)$$, $$f(i+1,j)$$ and $$f(i,j+2)$$,
we can start from $$f(m,n)$$ and calcuate $$f(0,0)$$ with a dynamic programming approach.

### Source Code

```python
class Solution(object):
    def isMatch(self, s, p):
        """
        :type s: str
        :type p: str
        :rtype: bool
        """
        m = len(s)
        n = len(p)
        prev = [None] * (n+1)
        cur = [None] * (n+1)

        for i in range(m, -1, -1):
            for j in range(n, -1, -1):
                if i == m and j == n:
                    cur[j] = True
                elif j == n:
                    cur[j] = False
                else:
                    match = i < m and (p[j] == '.' or p[j] == s[i])
                    if j < n-1 and p[j+1] == '*':
                        cur[j] = (match and prev[j]) or cur[j+2]
                    else:
                        cur[j] = match and prev[j+1]

            tmp = prev
            prev = cur
            cur = tmp

        return prev[0]
```

## Wildcard Matching

We can solve the wildcard matching problem with a similar approach. Since the definition of '*' is different now, we have
a similar but different $$isMatch$$ function.

$$
f(i,j) =
  \begin{cases}
    i = m, &\quad j = n \\
    (p[j] = '?' \lor p[j] = s[i]) \land f(i+1,j+1), &\quad p[j] \ne '*' \\
    f(i+1,j) \lor f(i,j+1), &\quad p[j] = '*'
  \end{cases}
$$

```python
class Solution(object):
    def isMatch(self, s, p):
        """
        :type s: str
        :type p: str
        :rtype: bool
        """
        m = len(s)
        n = len(p)
        prev = [None] * (n+1)
        cur = [None] * (n+1)

        for i in range(m, -1, -1):
            for j in range(n, -1, -1):
                if j == n:
                    cur[j] = i == m
                elif p[j] == '*':
                    if i == m:
                        cur[j] = cur[j+1]
                    else:
                        cur[j] = cur[j+1] or prev[j]
                else:
                    match = i < m and p[j] in {'?', s[i]}
                    cur[j] = match and prev[j+1]

            tmp = cur
            cur = prev
            prev = tmp

        return prev[0]
```
