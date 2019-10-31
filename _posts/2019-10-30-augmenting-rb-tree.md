---
layout: post
title:  "Order Statistic Tree and Interval Tree"
date:   2019-10-30
categories: [note]
tags:   [introduction to algorithms]
---

Order statistic tree and interval tree are two examples of augmented trees. If we use a self-balancing tree such as red-black tree as
the basic data structure, we can implement additional operations without negatively impacting the asymptotic worst caserunning time.

## Order Statistic Tree

Each node in an order statistic tree has an additional attribute: size. `x.size` means the number of nodes in the subtree rooted at `x`.
Namely we have `x.size = x.left.size + x.right.size + 1`. Because `x.size` can be obtained from only its two children, the asymptotic
running time of `Insertion` and `Deletion` operation does not change.
Order statistic tree supports two addtional operations.
`OS-Select(T, n)` returns the nth smallest element in the tree.
`OS-RANK(T, x)` returns the rank of element `x` in the tree.
Both of the operations run in `O(logn)` time which can be proved quite easily.
Order statistic tree can be used to solve [Josephus problem](https://en.wikipedia.org/wiki/Josephus_problem) in `O(nlogn)` time.

## Interval Tree

Interval tree stores intervals as objects. Each node `x` in the interval tree has `x.int` interval object and `x.max` the maximum endpoint
in the subtree rooted at `x`. Interval tree uses the lower endpoint of `x.int` as the key.
Interval tree can check if there is an interval in the tree that overlaps the input interval in `O(logn)` time.
