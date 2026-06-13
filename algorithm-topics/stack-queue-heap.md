---
description: Notes and typical questions for Stack, Queue or Heap related problems
icon: shelves
---

# Stack, Queue, Heap

## **Notes**

* When performing **stack-like** operations on a `String`, using a `StringBuilder` is often simpler and more efficient than using an explicit stack data structure.
* Although sliding windows questions are usually related to the 2-pointer solution. If the sliding windows question needs to compare numbers within the window, you also need to consider the solution: 2-pointer + **monotonic queue**.
* PruorityQueue
  * poll(): Remove the head item
* In Java, `ArrayDeque` is faster than `LinkedList` except for removing elements. Reference：[https://stackoverflow.com/questions/6163166/why-is-arraydeque-better-than-linkedlist](https://stackoverflow.com/questions/6163166/why-is-arraydeque-better-than-linkedlist)

## **Typical Questions (37)**

### **Mutual implementation between Queue and Stack (2)**

* LC 232. Implement Queue using Stacks
  * <pre><code># Analysis on amortized O(1) TC for pop
    # Assumption: When stack2 is empty, get pop calls for all items in the queue
    first pop:   O(2*n) transfer + O(1) pop
    other pops:  (n - 1) * O(1)  → O(n - 1)
    -------------------------------
    Total operations overall n pop calls: 2*n+1+n-1 = 3*n
    <strong>Amortized TC for pop: (3*n)/n ≈ O(1)
    </strong></code></pre>
* :orange\_circle: LC 225. Implement Stack using Queues
  * Approach 1: Use 1 queue. Straightforward
    * :thumbsup: 1.1 Push $$O(n)$$, Pop $$O(1)$$
      * [Optimal Answer](https://leetcode.com/problems/implement-stack-using-queues/submissions/1721167200/).
    * 1.2 Push $$O(1)$$, Pop $$O(n)$$. Not preferred compared to 1.1.
      * [Optimal Answer](https://leetcode.com/problems/implement-stack-using-queues/submissions/1721165082/).
  * Approach 2: Use 2 queues
    * 2.1 Push $$O(n)$$, Pop $$O(1)$$: **NOT straightforward**, queue1 is to store all elements **in stack order** with the help of queue2
      * [Optimal Answer](https://leetcode.com/problems/implement-stack-using-queues/submissions/1721157558/).
    * 2.2 Push $$O(1)$$, Pop $$O(n)$$. Not preferred compared to 2.1.

### **Normal Stack Common Use Cases (8)**

* Notes
  * Common cases
    * Matching / Pairing: resolve parentheses or symbols
    * Adjacent Merge / Reduction: repeatedly merge/remove neighbors based on a rule
    * Expression Evaluation: operators, precedence, calculators
    * Nested Structure Parsing: decode nested patterns
    * State Backtracking: undo previous state (path/string)
* LC 20. Valid Parentheses
  * The most elegant way is to push `) or ] or ]` when get `( or [ or {`. This way can simplify `if/else` logic
  * [Optimal Answer](https://leetcode.com/problems/valid-parentheses/submissions/1478181301). TC: $$O(n)$$, SC: $$O(n)$$
* LC 1047. Remove All Adjacent Duplicates In String
  * Approach 1: Use a stack, the most straightforward way
  * :thumbsup: Approach 2: Use 2 pointers, this way is better due to no space usage for the stack
* :white\_circle: LC 1209. Remove All Adjacent Duplicates in String II
  * [Optimal Answer](https://leetcode.com/problems/remove-all-adjacent-duplicates-in-string-ii/submissions/1963321853). TC: $$O(n)$$, SC: $$O(n)$$
* LC 150. Evaluate Reverse Polish Notation
* :white\_circle: LC 71. Simplify Path
  * [Optimal Answer](https://leetcode.com/problems/simplify-path/submissions/1559607285). TC: $$O(n)$$, SC: $$O(n)$$
* LC 2390. Removing Stars From a String
  * Stack approach: Use `StringBuilder` to simulate `Stack`. [Answer](https://leetcode.com/problems/removing-stars-from-a-string/submissions/1465358090). TC: $$O(n)$$, SC: $$O(n)$$
  * 2 pointers approach: [Answer](https://leetcode.com/problems/removing-stars-from-a-string/submissions/1465361947).
    * TC: $$O(n)$$
    * SC: $$pseudo-O(1)$$ due to the immutability of `String` in Java
* LC 735. Asteroid Collision
  * [Optimal Answer](https://leetcode.com/problems/asteroid-collision/submissions/1465372880). TC: $$O(n)$$, SC: $$O(n)$$
* :star2: :red\_circle: LC 394. Decode String
  * It's very hard to implement. I check the solution directly. Go through this test case "3\[a2\[c]2\[d]]" to understand why the solution works...
  * [Optimal Answer](https://leetcode.com/problems/decode-string/submissions/1465408938).
    * TC: $$O(max(k)*n)$$, where $$max(k)$$ is the max value of `k`, `n` is the size of the string array.
    * SC: $$O(n)$$.
* :orange\_circle: LC 224. Basic Calculator
  * It's **similar** to the above LC 394 question.
  * Hints
    * Try to resolve it using 1 stack.
      * Store signs ('+', '-') using an `int var` instead of a stack.
    * Try to handle numbers in the input string that have more than 1 digit without using a `while` loop
  * I finally made it by myself (I already saw the solution in previous rounds)!
  * [Optimal Answer.](https://leetcode.com/problems/basic-calculator/submissions/1509884058) TC: $$O(n$$), SC: $$O(n)$$
* :orange\_circle: LC 227. Basic Calculator II
  * Although it does not have `()`  , but it's more complicated than LC 224 due to `*/`&#x20;
  * [Optimal Answer](https://leetcode.com/problems/basic-calculator-ii/submissions/1897113275). TC: $$O(n)$$, SC: $$O(1)$$
* :orange\_circle: LC 1249. Minimum Remove to Make Valid Parentheses
  * Approach 1
    * I came up with this approach independently before checking the LeetCode editorial. The core idea is similar to the solution for **LC 224 (Basic Calculator).**
    * &#x20;[Answer](https://leetcode.com/problems/minimum-remove-to-make-valid-parentheses/submissions/1881029665). TC: $$O(n^2)$$, SC: $$O(n)$$.&#x20;
      * For TC, it's slow due to repeated string copying when merging nested builders. Conceptually, the process resembles: `b1.append(b2.append(...append(bk)...));` where deeply nested parentheses cause the same characters to be copied multiple times.
  * :thumbsup: Approach 2: [Optimal Answer](https://leetcode.com/problems/minimum-remove-to-make-valid-parentheses/submissions/1881049714). TC: $$O(n$$), SC: $$O(n)$$
* LC 2197. Replace Non-Coprime Numbers in Array
  * [Optimal Answer](https://leetcode.com/problems/replace-non-coprime-numbers-in-array/submissions/1944390135).  TC: $$O(nlogMax)$$, SC: $$O(n)$$

### **Normal Queue Common Use Cases (3)**

* LC 933. Number of Recent Calls
  * [Optimal Answer](https://leetcode.com/problems/number-of-recent-calls/submissions/1465450658). TC: $$O(n)$$, SC: $$O(n)$$
* :white\_circle: LC 649. Dota2 Senate
  * The solution with 2 queues is more clear and simpler.
  * [Optimal Answer](https://leetcode.com/problems/dota2-senate/submissions/1465461093). TC: $$O(n)$$, SC: $$O(n)$$
* LC 346. Moving Average from Data Stream
  * [Optimal Answer](https://leetcode.com/problems/moving-average-from-data-stream/submissions/1487510038). TC: $$O(1)$$, SC: $$O(n)$$
* :white\_circle: LC 362. Design Hit Counter
  * At first, I used binary search in `getHits()` and didn't remove anything in the queue because I didn't realize that `getHits()` is called with timestamps in increasing order as well.
  * Optimal Answer.&#x20;
    * TC: Both `hit()` and `getHits()`: amortized $$O(1)$$
    * SC: O(1). Max 300 items in the queue.
* :white\_circle: LC 2534. Time Taken to Cross the Door
  * [Optimal Answer](https://leetcode.com/problems/time-taken-to-cross-the-door/submissions/1970710899). TC: $$O(n)$$, SC: $$O(n)$$
* :white\_circle: LC 359. Logger Rate Limiter
  * [Optimal Answer](https://leetcode.com/problems/logger-rate-limiter/submissions/2032086291). TC: Amortized $$O(1)$$, SC: $$O(k)$$, k = number of unique messages in the last 10 seconds

### **Monotonic Queue (1)**

* :red\_circle: LC 239. Sliding Window Maximum
  * [Optimal Solution](https://leetcode.com/problems/sliding-window-maximum/submissions/1400187248). TC: $$O(n)$$, SC: $$O(k)$$

### Monotonic Stack (11)

* Use case: For an element in an array, when you need to find the index/value of the **1st element** to the **left/right** that is **greater/smaller than it**.
  * **Basic requirements for 1st Element**:
    * Example: Find the next greater element in elements after the current element.
    * Use a monotonic stack to maintain indices in an increasing or decreasing order (order is determined by the value of indexes) based on the requirement.
  * **Complex requirements for 1st Element**:
    * Example: Find the smallest element larger than the current element in the elements after it.
    *   Steps

        * Create another array storing the index of the original array and preprocessing it by sorting indices based on values of the original array and secondary by indices to ensure order.
        * Traverse sorted indices and use a stack to handle the 1st element condition.

        ```java
          // Sample code to find the smallest element larger than the current element in elements after it. 
          // Assume the original input array is called `arr`
          // Create another Integer array storing the index of the original array
          // Use Integer[] here bc Arrays.sort() method does not support lambda expression for primitive array type, e.g. int[]
          Integer[] indexArray = new Integer[n];
          for (int i = 0; i < n; i++) {
              indexArray[i] = i;
          }
          // Sort indexArray based on the value in original arr, breaking ties by index.
          Arrays.sort(indexArray, (a,b)-> arr[a] == arr[b] ? a-b : arr[a]-arr[b]);
          Integer[] result = new Integer[indexArray.length];
          Deque<Integer> stack = new ArrayDeque<>();
          for (int i = 0; i < indexArray.length; i++) {
              while (!stack.isEmpty() && stack.peekLast() < indexArray[i]) {
                  int polledIndex = stack.pollLast();
                  result[polledIndex] = indexArray[i];
              }
              stack.offerLast(indexArray[i]);
          }
          // Handle elements with no target by setting them to -1.
          while(!stack.isEmpty()) {
              int polledIndex = stack.pollLast();
              result[polledIndex] = -1;
          }
        ```

#### **Basic Monotonic Stack Problems**

* :star2: LC 739. Daily Temperatures
  * [Optimal Answer](https://leetcode.com/problems/daily-temperatures/submissions/1472219252/). TC: $$O(n)$$, SC: $$O(n)$$
* :white\_circle: LC 496. Next Greater Element I
  * [Optimal Answer](https://leetcode.com/problems/next-greater-element-i/submissions/1461045422/). TC: $$O(n)$$, SC: $$O(n)$$
* :orange\_circle: LC 503. Next Greater Element II
  * **Solve the circular problem by iterating the array twice.**
  * In round 3, I somehow tried to use the remaining items in the stack to solve the circular problem, but that's **NOT** the correct way.
  * Optimal Answer. TC: $$O(n)$$, SC: $$O(n)$$
* :orange\_circle: LC 901. Online Stock Span
  * [Optimal Solution](https://leetcode.com/problems/online-stock-span/submissions/1472223877)
    * TC: Amortized $$O(1)$$
    * SC: $$O(n)$$
* :white\_circle: LC 155. Min Stack
  * You can do the implementation with the `Stack` data structure.
  * Try to do it using only 1 stack.
  * [Optimal Answer](https://leetcode.com/problems/min-stack/submissions/1596981364). TC: $$O(1)$$ for each operation. SC: $$O(n)$$
* LC 3542. Minimum Operations to Convert All Elements to Zero
  * Key mental leap:&#x20;
    * Each operation eliminates all occurrences of a specific value within a contiguous region where no smaller value intervenes&#x20;
    * → a smaller value acts as a barrier that splits the same value into separate regions, each requiring its own operation
    * → so we maintain a strictly increasing stack of active segments, where each push is one operation.
  * Invariant: At any point during the left-to-right scan, the stack holds a strictly increasing sequence of distinct non-zero values, representing the "active layers" that\
    still need separate operations to eliminate.
  * [Optimal Answer](https://leetcode.com/problems/minimum-operations-to-convert-all-elements-to-zero/submissions/1977774798). TC: $$O(n)$$, SC: $$O(n)$$

#### **Trapping Rain Water Problems**

* :star2: LC 42. Trapping Rain Water
  * :white\_circle: Approach 1 with a stack
    * Accumulate the result by calculating the trapped water **horizontally**
    * When `height[i] == stack.peekLast()`, there are two valid approaches:
      1. Allow duplicate items in the stack: Push the current `height[i]` into the stack as usual.
      2. Keep only unique items in the stack: **First, remove the older duplicate from the stack.** Then, push the new `height[i]` into the stack. Reason: **The new item can serve as the left boundary for the next rectangle**, whereas the older duplicate is no longer useful.
    * [Optimal Solution](https://leetcode.com/problems/trapping-rain-water/submissions/1475561615). TC: $$O(n)$$, SC: $$O(n)$$
  * :orange\_circle: Approach 2 with 2 pointers
    * Accumulate the result by calculating the trapped water **vertically**
    * [Optimal Answer](https://leetcode.com/problems/trapping-rain-water/submissions/1769598902). TC: $$O(n)$$, SC: $$O(1)$$

#### **Largest Rectangle Problem**

* :star2: :red\_circle: LC 84. Largest Rectangle in Histogram
  * It's a reversed version of LC 42.
  * It's easy to make mistakes when getting the width of the rectangle.
  * [Optimal Answer](https://leetcode.com/problems/largest-rectangle-in-histogram/submissions/1497894960/). TC: $$O(n)$$, SC: $$O(n)$$
* :red\_circle: LC 85. Maximal Rectangle
  * It's a genius solution based on LC 84 above
  * [Optimal Solution](https://leetcode.com/problems/maximal-rectangle/submissions/1485217147). TC: $$O(m*n)$$, SC: $$O(n)$$

#### **Advanced Monotonic Stack Problems**

* :star2: :red\_circle: LC 962. Maximum Width Ramp
  * This problem can also be resolved by **2 pointers + `rightMax` array** (see that section). It's necessary to grasp this approach as well.
  * The monotonic stack is used for storing starting points. Need another array iteration from the end of the array to check valid results
  * [Optimal Solution](https://leetcode.com/problems/maximum-width-ramp/submissions/1491036080). TC: $$O(n)$$, SC: $$O(n)$$
* :star2: :red\_circle: LC 2863. Maximum Length of Semi-Decreasing Subarrays
  * This question is the same as LC 962
  * Approach 1: Monotonix Stack. TC: $$O(n)$$, SC: $$O(n)$$
  * Approach 2: 2 pointers + `rightMin` array. TC: $$O(n)$$, SC: $$O(n)$$
* :red\_circle: LC 975. Odd Even Jump
  * This solution is based on **DP + Monotonic Stack** and this question can also be solved by **DP + TreeMap**
  * [Optimal Solution](https://leetcode.com/problems/odd-even-jump/submissions/1491970338). TC: $$O(n*log{n})$$, SC: $$O(n)$$

### Monotonic Deque (1)

* :red\_circle: LC 3420. Count Non-Decreasing Subarrays After K Operations
  * This question is super hard and even the solution is very hard to understand. Add some comments in the optimal answer and go through some examples to get the idea.
    * I'm still not sure why reversing the array is more efficient.
  * [Optimal Answer](https://leetcode.com/problems/count-non-decreasing-subarrays-after-k-operations/submissions/1527954906/?envType=company\&envId=google\&favoriteSlug=google-three-months). TC: $$O(n)$$, SC: $$O(n)$$

### **Heap**&#x20;

* Notes
  * Whenever you see that you need to choose the **k smallest or the k largest** among a group of numbers, always consider using a heap(priority queue).

#### **Lazy Update Heap Problems**

* Notes: Use lazy update in a heap when you need to repeatedly extract the min/max, but elements’ priorities can **change due to updates** (e.g., merge, delete, or value change), and the heap does NOT support efficient in-place updates. Instead of modifying existing entries, push new ones and treat old entries as stale, then validate and discard them when they are popped.
* :orange\_circle: LC 3510. Minimum Pair Removal to Sort Array II
  * [Optimal Answer](https://leetcode.com/problems/minimum-pair-removal-to-sort-array-ii/submissions/1979686177/). TC: $$O(nlogn)$$, SC: $$O(n)$$

#### **Common Heap Problems**

* :star2: LC 347. Top K Frequent Elements
  * Learn how to initialize `PriorityQueue` with a custom `Comparator`
  * [MinHeap Answer](https://leetcode.com/problems/top-k-frequent-elements/submissions/1722376209/): TC $$O(n*log{k})$$, SC: $$O(n+k)$$
* :star2: LC 215. Kth Largest Element in an Array
  * [MinHeap Solution](https://leetcode.com/problems/kth-largest-element-in-an-array/submissions/1468831794). TC: $$O(n*log{k})$$, SC: $$O(k)$$
  * :orange\_circle: [Counting Sort Solution](https://leetcode.com/problems/kth-largest-element-in-an-array/submissions/1468838317).
    * TC: $$O(n+m)$$, where $$n$$ is the length of `nums` and $$m$$ is `maxValue - minValue`
    * SC: $$O(m)$$, $$m$$ is `maxValue - minValue`
* :orange\_circle: LC 2336. Smallest Number in Infinite Set
  * [Optimal Answer](https://leetcode.com/problems/smallest-number-in-infinite-set/submissions/1468849771).
    * $$n$$ is the number `addBack(num)` and $$m$$ is the number of `popSmallest()` method calls.
    * TC: $$O((m+n)*logn)$$
    * SC: $$O(n)$$
* :red\_circle: LC 2542. Maximum Subsequence Score
  * Idea
    * k-1 largest numbers of `nums2` will never be selected. For the selected number from `nums2` in each possible score combination, it can only be the kth largest number or all other numbers which < kth largest number in `nums2`
    * For each possible score combination, the questions have 2 requirements (1 for `nums1`, 1 for `nums2`). It's impossible to consider both 2 requirements at the same time. Therefore, we need to fix 1 requirement first and sort out another requirement at the same time. Since we know the specific enumeration of the selected numbers in nums2, we can first fix the chosen numbers from nums2. Then, we can dynamically select the numbers from nums1 using a `minHeap`.
  * [Optimal Answer](https://leetcode.com/problems/maximum-subsequence-score/submissions/1468874885). TC: $$O(n * log{n})$$. SC: $$O(n)$$
* :orange\_circle: LC 2462. Total Cost to Hire K Workers
  * Very easy to **make mistakes** during **implementation**.
  * [Optimal Answer](https://leetcode.com/problems/total-cost-to-hire-k-workers/submissions/1468933530)
    * For the sake of brevity, let m be the given integer candidates
    * TC: $$O((k+m)*log{m})$$
    * SC: $$O(m)$$
* :star2: :orange\_circle: LC 253. Meeting Rooms II
  * [Optimal Answer](https://leetcode.com/problems/meeting-rooms-ii/submissions/1478231315). TC: $$O(n*log{n})$$, SC: $$O(n)$$
* :orange\_circle: LC 2402. Meeting Rooms III
  * [Optimal Answer](https://leetcode.com/problems/meeting-rooms-iii/submissions/1510099644)
    * TC: $$O(M*logM + M*logN)$$
      * > For inner `while` loop, It will have a maximum of `N` iterations each time, but it can't have `N` iterations every time. We can't pop more items than we have previously pushed, and we only push one 1 item per outer loop. Since we only push `M` times, we can only pop `M-1` times over the whole function duration.
    * SC: $$O(N)$$
* :white\_circle: LC 1509. Minimum Difference Between Largest and Smallest Value in Three Moves
  * Approach 1: Full sorting + check result
  * Approach 2 (better): Partial sorting using heap + check result
    * [Optimal Solution](https://leetcode.com/problems/minimum-difference-between-largest-and-smallest-value-in-three-moves/submissions/1497883896). TC: $$O(n)$$, SC: $$O(1)$$
* :star2: :white\_circle: LC 295. Find Median from Data Stream
  * [Optimal Answer](https://leetcode.com/problems/find-median-from-data-stream/solutions/74047/java-python-two-heap-solution-o-log-n-add-o-1-find). TC: $$O(logn)$$, SC: $$O(n)$$
* :star2: LC 23. Merge k Sorted Lists
  * Approach 2 is better, but its implementation is trickier.
  * Approach 1 using Heap: [Optimal Answer](https://leetcode.com/problems/merge-k-sorted-lists/submissions/1529052478/?envType=company\&envId=google\&favoriteSlug=google-three-months).
    * Let $$N$$ be the total number of nodes and $$K$$ be the number of lists
      * TC: $$O(N*log{K})$$, SC: $$O(K)$$
  * Approach 2 using Divide & Conquer: [Optimal Answer](https://leetcode.com/problems/merge-k-sorted-lists/submissions/1869794762). TC: $$O(N*log{K})$$, SC: $$O(1)$$
* :red\_circle: LC 502. IPO
  * I came up with a [solution](https://leetcode.com/problems/ipo/submissions/1872624387) that gets TLE. The problem is that I rebuilt the “feasible set” from scratch each round when choosing projects.
  * [Optimal Answer](https://leetcode.com/problems/ipo/submissions/1872638131). TC: $$O(n*logn)$$, SC: $$O(n)$$
* :orange\_circle: LC 373. Find K Pairs with Smallest Sums
  * [Optimal Answer](https://leetcode.com/problems/find-k-pairs-with-smallest-sums/submissions/1874696731). TC: $$O(k*logk)$$, SC: $$O(k)$$
* :star2: :red\_circle: LC 407. Trapping Rain Water II
  * Optimal Answer. TC: $$O(m*n*log(m*n))$$, SC: $$O(m*n)$$
* :white\_circle: LC 2163. Minimum Difference in Sums After Removal of Elements
  * [Optimal Answer](https://leetcode.com/problems/minimum-difference-in-sums-after-removal-of-elements/submissions/1934318331). TC: $$O(n*logn)$$, SC: $$O(n)$$
