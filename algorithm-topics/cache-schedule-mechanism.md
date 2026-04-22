---
description: Notes and typical questions for Cache & Priority mechanism
icon: hourglass-clock
---

# Cache & Priority Systems

## **Notes**

These problems require maintaining a dynamically changing set of items ordered by some ranking rule (recency, frequency, priority, etc.), while supporting fast add, update, delete, and retrieval operations.

These problems combine:

* O(1) lookup (HashMap)
* Ordered maintenance (Heap / DLL / TreeMap)
* State mutation (priority/frequency/recency changes)

Focus:

* Maintain invariants
* Handle tie-breaking
* Coordinate multiple data structures correctly
* Understand space tradeoffs (lazy deletion vs strict removal)

## **Typical Questions**

### **Others**

* :star2: :orange\_circle: LC 146. LRU Cache
  * Idea: Implement with Map + Double Linked List (2 dummy nodes for head and tail, respectively)
  * Pitfalls
    * Connect the head and tail in the constructor
    * For `put` , it can be adding a new node or updating an existing node.
  * [Optimal Answer](https://leetcode.com/problems/lru-cache/submissions/1472922731).
    * TC: $$O(1)$$ for both `get` and `put`
    * SC: $$O(capacity)$$
* :orange\_circle: LC 432. All O\`one Data Structure
  * I only wrote a standard LRU solution. The reason I failed to come up with an O(1) solution
    * Missing the “only ±1 changes” leverage: Counts only changes by **+1 or -1** each operation. That’s the crucial property that screams “adjacent bucket moves.” If you don’t consciously look for that kind of property, you’ll design a general reordering solution (yours), not a local-move solution (optimal).
  * [Optimal Answer](https://leetcode.com/problems/all-oone-data-structure/submissions/1918559933).&#x20;
    * TC: $$O(1)$$ for all methods
    * SC: $$O(n)$$
* :star2: :red\_circle: LC 460. LFU Cache
  * Idea
    * Implement with 2 Maps
    * To get the LRU result when there is a tie, use **`LinkedHashSet()`**
  * [Optimal Answer](https://leetcode.com/problems/lfu-cache/submissions/1473194931/)
    * TC: $$O(1)$$ for both `get` and `put`
    * SC: $$O(capacity)$$
* :orange\_circle: LC 3408. Design Task Manager
  * Approach 1 - TreeMap+TreeSet:
    * [Answer](https://leetcode.com/problems/design-task-manager/submissions/1918437718)
      * TC: $$O(logn)$$ for all `add`, `edit`, `rmv`, `execTop`&#x20;
      * SC: $$O(n)$$, only contains active tasks
  * :thumbsup: Approach 2 - Map+Heap with lazy deletion
    * [Optimal Answer](https://leetcode.com/problems/design-task-manager/submissions/1918442263).
      * TC:
        * &#x20;$$O(logn)$$ for `add`, `edit`,&#x20;
        * $$O(1)$$ for `rmv`
        * Amortized $$O(logn)$$ for `execTop`
      * SC: $$O(n+m)$$, may contain stale tasks in the heap.
* LC 716. Max Stack
  * [Optimal Answer](https://leetcode.com/problems/max-stack/submissions/1962252924).
    * TC: $$O(1)$$ for `top` , $$O(logn)$$ for others
    * SC: $$O(n)$$

### Dynamic Top-K Maintenance

* :white\_circle: LC 3318. Find X-Sum of All K-Long Subarrays I
  * The idea is straightforward and just implementation is kind of long...
  * [Optimal Answer](https://leetcode.com/problems/find-x-sum-of-all-k-long-subarrays-i/submissions/1481704262)
    * TC: $$O(n*k*log{x})$$
    * SC: $$O(k+x)$$
* :red\_circle: LC 3321. Find X-Sum of All K-Long Subarrays II
  * :zap::zap::zap:Key trigger: If the answer depends on a dynamic top-k subset, try maintaining **two balanced and ordered groups** instead of recomputing the subset every time.
  * [Optimal Answer](https://leetcode.com/problems/find-x-sum-of-all-k-long-subarrays-ii/submissions/1984956229). TC: $$O(nlogk)$$, SC: $$O(k)$$
