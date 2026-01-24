---
description: Notes and typical questions for cache schedule mechanism
icon: hourglass-clock
---

# Cache Schedule Mechanism

## **Notes**

* Placeholder

## **Typical Questions**

* :star2: :orange\_circle: LC 146. LRU Cache
  * Idea: Implement with Map + Double Linked List (2 dummy nodes for head and tail, respectively)
  * Pitfalls
    * Connect the head and tail in the constructor
    * For `put` , it can be adding a new node or updating an existing node.
  * [Optimal Answer](https://leetcode.com/problems/lru-cache/submissions/1472922731).
    * TC: $$O(1)$$ for both `get` and `put`
    * SC: $$O(capacity)$$
* :star2: :red\_circle: LC 460. LFU Cache
  * Idea
    * Implement with 2 Maps
    * To get the LRU result when there is a tie, use **`LinkedHashSet()`**
  * [Optimal Answer](https://leetcode.com/problems/lfu-cache/submissions/1473194931/)
    * TC: $$O(1)$$ for both `get` and `put`
    * SC: $$O(capacity)$$
