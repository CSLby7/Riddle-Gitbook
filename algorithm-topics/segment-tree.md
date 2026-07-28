---
description: Notes and typical questions for Segment Tree related questions
icon: list-tree
---

# Segment Tree

## Notes

* Introduction: https://www.bilibili.com/video/BV1cb411t7AM/?share\_source=copy\_web\&vd\_source=28fd44c5c9b62466ed4422197e99ce77
* Segment Tree **Size** — Why `4*n` Is Enough
  * A segment tree is a **binary tree** built over an array of length `n`.
  * Leaves represent **single elements**; Parent nodes represent **ranges**.
  * If `n` is not a power of 2, the tree is built as if the array length were the **next power of two** `L ≥ n`.
  * A full binary tree with `L` leaves has **`2*L − 1` nodes**.
  * For any `n`, the next power of two satisfies **`L < 2*n`**.
  *   Therefore, total nodes:

      ```
      ≤ 2L − 1 < 2 * (2n) = 4n
      ```
  * So allocating an array of size **`4 * n`** always guarantees enough space.
* If the problem asks “Find the smallest index > x".
  * Think: **`TreeSet.higher(x)`** first. _**NOT**_ range sum + binary search
  * Even if you want to use the segment tree, you must extend the template to support a **“find first index in range satisfying a condition”** operation, instead of doing binary search + multiple range queries—for example, LC 1488.
    * The node must store enough aggregate info to determine whether the current segment may contain a valid answer (e.g., sum/max/min).
    * During query, first check feasibility, then descend left-first to locate the smallest valid index.
    * This keeps each operation `O(logn)` instead of `O(log²n)`.

## **Typical Questions**

### Lazy Propagation & Tree Search

* Notes
  * Lazy Propagation: Supports **range updates** (e.g. range add / range assignment) in `O(log n)`.
    * Defers updates to child nodes until they are actually needed.
    * Introduces **lazy tags** along with `push()` and `pull()`.
  * Tree Search: Instead of returning an aggregate value (sum / min / max), traverses the segment tree to **locate an index** satisfying some condition in `O(log n)`.
    * Common examples:
      * Find the first/last position satisfying a condition.
      * Find the k-th element.
      * Find the first value ≥ x.
* LC 3719. Longest Balanced Subarray I
  * [Answer](https://leetcode.com/problems/longest-balanced-subarray-i/submissions/2080215603) (Not optimal answer. See optimal answer in v2 of this problem). TC: $$O(n^2)$$, SC: $$O(n)$$
* :red\_circle: LC 3721. Longest Balanced Subarray II
  * It's toooo hard.
  * [Optimal Answer](https://leetcode.com/problems/longest-balanced-subarray-ii/submissions/2081253686). TC: $$O(nlogn)$$, SC: $$O(n)$$

### **Max Segment Tree**

* LC 3477. Fruits Into Baskets II
  * Same as below.
  * [Optimal Answer](https://leetcode.com/problems/fruits-into-baskets-ii/submissions/1903917165/).
  * TC: $$O(n+n*((log{n})^2+log{n})) => O(n*log{n})$$
  * SC: $$O(n)$$
* :red\_circle: TC 3479. Fruits Into Baskets III
  * [Optimal Answer](https://leetcode.com/problems/fruits-into-baskets-iii/submissions/1903683170).
  * TC: $$O(n+n*((log{n})^2+log{n})) => O(n*log{n})$$
  * SC: $$O(n)$$

