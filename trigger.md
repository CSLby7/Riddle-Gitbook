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
  * Need exact top k set OR frequent arbitrary removal → **Two balanced sets/treeSets** (LC 3321, LC 3013)
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

## 4. Prefix Index Mod Pattern

When you see&#x20;

* subarray length divisible by k&#x20;
* OR length has a modulo constraint

Think: `length = r - l` using prefix indices → modulo condition on length becomes modulo condition on prefix indices

Core Insight: `(r - l) % k == 0` → `r % k == l % k` → group prefix sums by `index % k`

For max sum: current prefix - min previous prefix in the same group (Example questions: LC 3381)

## 5. Tree Component Aggregation Pattern

When you see&#x20;

* Tree&#x20;
* AND remove edges / split into components / count valid components&#x20;
* AND each component’s validity depends on an aggregated value: sum / size / average / product / modulo / max-min

Think: This is not path exploration. This is bottom-up aggregation.

Core question: What information does each branch need to **carry over to its parent/neighbor**

* Common carry-over values: sum count remainder subtree size best value from subtree

Decision:&#x20;

* If a branch already satisfies the condition, → cut it / count it / stop passing it upward.
* If a branch does not satisfy the condition, → it cannot stand alone, → carry its aggregated value upward, and merge with the parent/neighbor.

Trigger: When the problem asks about the value of a connected component, do not think “which direction should I explore?” Think “what does this completed branch hand back?”

Example questions:&#x20;

* LC 2872. Maximum Number of K-Divisible Components&#x20;
* LC 2265. Count Nodes Equal to Average of Subtree&#x20;
* LC 1339. Maximum Product of Splitted Binary Tree

## 6. Alternating String/Array

**Invariant to maintain state -> Index parity**

* For an alternating string, the value at each position is completely determined by its index parity.

