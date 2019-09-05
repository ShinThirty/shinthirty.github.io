---
layout: post
title:  "Tree Traversal without Recursion or Stack"
date:   2019-09-04
categories: [note]
tags:   [tree]
---
<script src='https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.5/MathJax.js?config=TeX-MML-AM_CHTML' async></script>

According to wikepedia page [Tree traversal](https://en.wikipedia.org/wiki/Tree_traversal),

> With the iterative implementations we can remove the stack requirement by maintaining parent pointers in each node.

A related problem is asked in Chapter 10 of *Introduction to Algorithms*:

> Write an $$O(n)$$ time nonrecursive procedure that, given an n-node binary tree, prints out the key of each node.
> Use no more than constant extra space outside of the tree itself and do not modify the tree, even temporarily, during the procedure.

As said in the wikipedia quote, we can traverse an n-node binary without recursion or additional stack space if we maintain a
parent pointer in each tree node. The concrete algorithm is:

* Initialize two pointers, `prev` and `cur`. Initial value of `prev` is `NIL` while initial value of `cur` is `root`.

* Evaluate `prev` and `cur`, determine where to go next:

  * If `prev` == `NIL` or `prev` == `cur.p`, the subtree rooted at `cur` is unvisited. Descend to `cur.l` if `cur.l` is not `NIL`, otherwise descend to `cur.r`. If both `cur.l` and `cur.r` are `NIL`, ascend to `cur.p`.

  * If `prev` == `cur.l`, the subtree rooted at `cur.l` is visited. The means the left subtree of `cur` is visited so we should descend to `cur.r`. If `cur.r` == `NIL`, ascend to `cur.p`.

  * If `prev` == `cur.r`, the subtree rooted at `cur.r` is visited. Because we only visit the right subtree after visiting the left subtree, the subtree rooted at `cur.l` is also visited. This means the subtree rooted at `cur` is visited and we should ascend to `cur.p`.

  * When ascending to `cur.p` and `cur.p` == `NIL`, traversal is completed.

This procedure finishes the traversal in $$O(n)$$ time and only uses two addtional pointers `prev` and `cur`. We can implement pre-order, in-order and post-order based on when we process the `cur` node.

* Pre-order: process `cur` when descending to `cur.l`

* In-order: process `cur` when descending to `cur.r`

* Post-order: process `cur` when ascending to `cur.p`
