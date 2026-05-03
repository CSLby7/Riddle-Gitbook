---
icon: bolt-lightning
---

# Trigger

## 1. Top-K Pattern

When you see

* need "top k" / "best k" / "most frequent k"
* OR answer depends only on a subset of size k
* AND elements are changing (sliding window / updates / frequency changes)

Think: Maintain a boundary between selected (top k) and unselected

Decide:

* Static or only insertion → heap (LC 347)
* Dynamic updates:
  * Only need top element OR lazy deletion is acceptable → **Heap** (lazy deletion)
  * Need exact top k set OR frequent arbitrary removal → **Two balanced sets/treeSets** (LC 3321)
  * Need median / split into two halves → Two heaps

## 2. Intervals Pattern

When you see

* Intervals
* Meetings

Decide:

* What does overlap mean here?
  * Merge into one structure
    * Singal: Output is merged ranges/partitions
    * Sort by start -> maintain active interval
    * LC 56, 57, 228, 763
  * Can coexist / can be handled together
    * Signal: choose max compatible, min removals, min groups
    * Usually sort by end -> keep the smaller end
    * LC 435, 452, 252
  * Previously chosen points can be reused
    * Signal: need to know how many selected elements are inside interval
    * Sort by end -> if under-covered, add points from right
    * LC 757

Core Insight

* start sort → maintain structure
* end sort → greedy decision

## 3. Two-Sequence DP Pattern

When you see&#x20;

* two strings / two arrays&#x20;
* AND choices must preserve relative order&#x20;
* AND the answer depends on **matching, aligning, pairing**, or **transforming** both sequences

Think: 2D prefix DP / LCS-style DP

Decide: What does dp\[i]\[j] mean? Usually: best answer using seq1\[0..i] and seq2\[0..j]

Transition shape: What are the choices at (i, j)?&#x20;

* Pair / match / use both&#x20;
* Skip seq1\[i]&#x20;
* Skip seq2\[j]

Non-empty requirement: If empty choice is not allowed, do not initialize answer as 0. When taking a pair, allow starting fresh from current pair.

Example questions: LC 1143, 72, 1458

