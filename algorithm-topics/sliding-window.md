---
description: Notes and typical questions for sliding window algorithm
icon: rectangle-vertical-history
---

# Sliding Window

## **Sliding Window (1D) General**

### **Questions**

* :white\_circle: LC 643. Maximum Average Subarray I
  * [Optimal Answer](https://leetcode.com/problems/maximum-average-subarray-i/submissions/1463823615); TC: $$O(n)$$, SC: $$O(1)$$
* LC 1456. Maximum Number of Vowels in a Substring of Given Length
  * [Optimal Answer](https://leetcode.com/problems/maximum-number-of-vowels-in-a-substring-of-given-length/submissions/1464546660); TC: $$O(n)$$, SC: $$O(1)$$
* :white\_circle: LC 3350. Adjacent Increasing Subarrays Detection II
  * [My Answer](https://leetcode.com/problems/adjacent-increasing-subarrays-detection-ii/submissions/1534325693). TC:  $$O(n)$$ with multiple passes, SC: $$O(n)$$
  * [Optimal Answer](https://leetcode.com/problems/adjacent-increasing-subarrays-detection-ii/solutions/6028753/java-c-python-one-pass-o-1-space). TC: $$O(n)$$, SC: $$O(1)$$
* LC 1695. Maximum Erasure Value
  * [Optimal Answer](https://leetcode.com/problems/maximum-erasure-value/submissions/1973867371). TC: $$O(n)$$, SC: $$O(m)$$
* :orange\_circle: LC 1888. Minimum Number of Flips to Make the Binary String Alternating
  * **Key Insight:**&#x20;
    * My initial solution simulated flips from left to right, where the decision for each character depended on the corrected value of the previous character. This created a **sequential dependency**, making the state **impossible** to update incrementally when the sliding window moved—removing the leftmost character could invalidate the entire computation.
    * The correct approach is to **redefine the state**. Instead of tracking the flip process, represent the answer as the **sum of independent per-index contributions** (mismatches against the **two fixed alternating patterns**). Once each index contributes independently, a sliding window only needs to remove the left contribution and add the right contribution, reducing the complexity from **O(n²)** to **O(n)**.
  * [Optimal Answer](https://leetcode.com/problems/minimum-number-of-flips-to-make-the-binary-string-alternating/submissions/2058561844). TC: $$O(n)$$, SC: $$O(1)$$
* LC 1151. Minimum Swaps to Group All 1's Together
  * [Optimal Answer](https://leetcode.com/problems/minimum-swaps-to-group-all-1s-together/submissions/2059914258/). TC: $$O(n)$$, SC: $$O(1)$$
* :orange\_circle: LC 3013. Divide an Array Into Subarrays With Minimum Cost II
  * [Optimal Answer](https://leetcode.com/problems/divide-an-array-into-subarrays-with-minimum-cost-ii/submissions/2074056931). TC: $$O(nlogdist)$$, SC: $$O(dist)$$
* :white\_circle: LC 1291. Sequential Digits
  * [Optimal Answer](https://leetcode.com/problems/sequential-digits/submissions/2108204943). TC: $$O(1)$$, SC: $$O(1)$$

## **Sliding Window (1D) Subarray/Substring Search Meeting With Requirements**

### Notes

* Two-pointers are also useful when you need to **explore a set of subarrays/substrings that meet certain conditions** in a given input array/string and calculate results while exploring subarrays. For this kind of question, you usually need to use a fast point to explore the array and move the left pointer when the subarray does not meet the condition.

### :jigsaw: **Sliding Window with Aggressive Shrinking**

#### Notes

* You may need to use **`while` loop to move the left pointer until the subarray meets the condition**.

#### Questions

* LC 3. Longest Substring Without Repeating Characters
  * Approach 1: Normal 2 pointers.
    * [Answer](https://leetcode.com/problems/longest-substring-without-repeating-characters/submissions/1474875184). TC: $$O(2*n)=O(n)$$, SC: $$O(1)$$
  * :thumbsup: :white\_circle: Approach 2: Optimized 2-pointers. Reduce the inside `while` loop from the outside `for` loop. If the window has duplicates, We can move the left pointer directly to the right element of the duplicated one. Since this way will **skip removing elements from `Map`**, we need to **ensure the index of duplicates gets from `Map` is within the window**.
    * [Optimal Answer](https://leetcode.com/problems/longest-substring-without-repeating-characters/submissions/1474880775). TC: $$O(n)$$, SC: $$O(1)$$
* :star2: :white\_circle: LC 209. Minimum Size Subarray Sum
  * [Optimal Answer](https://leetcode.com/problems/minimum-size-subarray-sum/submissions/1778430693). TC: $$O(n)$$, SC $$O(1)$$
* :red\_circle: LC 904. Fruit Into Baskets
* :red\_circle: LC 567. Permutation in String
  * Be careful that there are 2 invalid cases (1. character is not in the target string, 2. character is in the target string but already occurred in windows previously)
  * if it is the 2nd invalid case, after taking actions, it may become a valid case!
  * Therefore, we should always check if it is a valid case at the end of each iteration
* :red\_circle: LC 3346. Maximum Frequency of an Element After Performing Operations I
  * I made some progress. I realized the input array needs to be sorted first, and get an $$O(n^2)$$ idea for the 1st case below, but then I got stuck.
  * 2 cases for the central point (the value that elements get updated to)
    * It's an existing element
      * **After sorting, for each element `e` in the array, there is a technique to find the number of elements within the range `[e-k,e+k]` in** $$O(n)$$ **by scanning the array once.**
    * It's a value that does not exist in the input array
  * [Optimal Answer](https://leetcode.com/problems/maximum-frequency-of-an-element-after-performing-operations-i/submissions/1515093798). TC: $$O(n*log{n})$$, SC: $$O(n)$$
* :white\_circle: LC 2762. Continuous Subarrays
  * There is another optimal answer that only uses 2 pointers without `TreeMap` . Since it has the same TC and SC as my answer and it's more complicated to understand, I did not use it.
  * [Optimal Answer](https://leetcode.com/problems/continuous-subarrays/submissions/1562157563).
    * Let $$n$$ be the size of the input, and $$k$$ be the size of `TreeMap` . Since $$k$$ should always <= 3 based on the requirement of the question, we can treat $$k$$ as a constant
    * TC: $$O(n*log{k}) => O(n)$$
    * SC: $$O(k) => O(1)$$
* :red\_circle: LC 30. Substring with Concatenation of All Words
  * Check explanation: [https://leetcode.com/problems/substring-with-concatenation-of-all-words/description/](https://leetcode.com/problems/substring-with-concatenation-of-all-words/description/)
  * **Be careful about comparing `Integer` !!!**
  * The inner loop uses the sliding window idea.
  * [Optimal Answer](https://leetcode.com/problems/substring-with-concatenation-of-all-words/submissions/1781837472).
    * Given $$n$$ as the length of `s`, $$a$$ as the length of `words`, and $$b$$ as the length of each word:
      * TC: $$O(a+n*b)$$, SC: $$O(a+b)$$
* :star2: :red\_circle: LC 76. Minimum Window Substring
  * Common mistake when simply using the normal sliding window idea
    * Pitfall: Cannot simply move the left pointer when the right pointer points to such a `char c` (String t has c with number k, and we already see k times of `c` in the current window). Reason is that **it's possible to have k+1 times of `c` in the final answer window**. For example, s="abbc", t="abc"
    * Solution: Core idea to resolve concerns above: Once you have a **valid** window, **aggressively** move the left pointer until it becomes **invalid**.
  * Answer
    * :thumbsup: Approach 1 with core idea above: [Optimal Answer](https://leetcode.com/problems/minimum-window-substring/submissions/1381629522). TC: $$O(n)$$, SC: $$O(1)$$
    * Approach 2 with an alternative idea: [Answer](https://leetcode.com/problems/minimum-window-substring/submissions/1858369183). TC: $$O(n)$$, SC: $$O(1)$$
* :orange\_circle: LC 2106. Maximum Fruits Harvested After at Most K Steps
  * Approach 1 with TreeMap (my own solution)
    * [Answer](https://leetcode.com/problems/maximum-fruits-harvested-after-at-most-k-steps/submissions/1922874694). TC : $$O(nlogn)$$, SC: $$O(n)$$
  * Approach 2 with Binary Search
    * Implementation trick: Use `prefixSum[n+1]`, which means `prefix[i]` represents the sum of elements in the half-open range `[0, i)` (i.e., before index `i`).
    * [Answer](https://leetcode.com/problems/maximum-fruits-harvested-after-at-most-k-steps/submissions/1923997390/). TC: $$O(n+klogn)$$, SC: $$O(n)$$
  * :thumbsup: Approach 3 with Sliding Window
    * [Optimal Answer](https://leetcode.com/problems/maximum-fruits-harvested-after-at-most-k-steps/submissions/1926749800/). TC: $$O(n)$$, SC: $$O(1)$$
* LC 3634. Minimum Removals to Balance Array
  * [Optimal Answer](https://leetcode.com/problems/minimum-removals-to-balance-array/submissions/2085472334). TC: $$O(nlogn)$$, SC: $$O(logn)$$

### :jigsaw: **Sliding Window with Non-Aggressive Shrinking**

#### Notes

* You may **NOT use `while` loop to move the left pointer until the subarray meets the condition** and **NOT shrink the window below the max window size found previously**.

#### Questions

* :star2: :white\_circle: LC 1004. Max Consecutive Ones III
  * Think it this way instead: Find the max window which includes at most k 0's
    * Straightforward idea: Have a 2 loops. Outer loop to explore array. When the window is invalid, the inner loop is used to keep reducing windows from the left side until it becomes valid. [Answer](https://leetcode.com/problems/max-consecutive-ones-iii/submissions/1464575090). TC: $$O(n)$$, SC: $$O(1)$$
    * Improved idea: No need for the inner loop. when the window becomes invalid, `j - i` effectively represents the current max window size. We **don’t need to keep shrinking** the window from the left until it becomes valid; we only need to **maintain the current size and slide the window forward**. Once the window becomes valid again after a shift, we can naturally continue expanding it. [Answer](https://leetcode.com/problems/max-consecutive-ones-iii/submissions/1464585667). TC: $$O(n)$$, SC: $$O(1)$$
* :white\_circle: LC 1493. Longest Subarray of 1's After Deleting One Element
  * Basically same as above LC 1004
  * [Optimal Answer](https://leetcode.com/problems/longest-subarray-of-1s-after-deleting-one-element/submissions/1464587930). TC: $$O(n)$$, SC: $$O(1)$$.
* :red\_circle: LC 424. Longest Repeating Character Replacement
  * The idea of not shrinking window size is similar to LC 1004
    * When finding the first valid window, assume the window size is `l` and the max frequency of characters within this window is `maxFreq`. Valid window means `l-maxFreq <= k`
    * In the next round,
      * Increase windows by moving `end` index to the right by 1.
      * If new `l+1` length window becomes invalid now, we just need to move `start` index to right by 1 and update the frequency map.
      * Then the window size becomes to `l` again but this new `l` size window may be **INVALID** and `maxFreq` may be **STALE**.
      * However, we do NOT care about these 2 issues. Since we want to find the max window, we can just **use the previous valid max window size to scan the array**.
      * **If there is a larger valid window size (> `l`), there must be a larger `maxFreq` because this equation `l-maxFreq <= k`. Only when `maxFreq` becomes larger, `l` can be larger as well.**
      * That's also why we do **NOT need to consider decreasing `maxFreq`** when moving `start` index and do **NOT care if it is stale**. We **ONLY care and want to find a larger `maxFreq`**&#x20;

## **Sliding Window (2D)**

### **Notes**

Used when processing every fixed-size `k × k` (or `h × w`) submatrix in a matrix.

**Core idea:** Adjacent windows share most of their elements. Instead of rebuilding each window from scratch, update only the rows/columns that enter or leave.

* **Move right:** remove the leftmost column, add the new rightmost column.
* **Move left:** remove the rightmost column, add the new leftmost column.
* **Move down:** remove the top row, add the new bottom row.
* **Snake traversal** can avoid jumping from the end of one row back to the beginning of the next.

### Questions

* :orange\_circle: LC 3567. Minimum Absolute Difference in Sliding Submatrix
  * Approach 1 - Brute force
    * [Answer](https://leetcode.com/problems/minimum-absolute-difference-in-sliding-submatrix/submissions/2124267775). TC: $$O((m-k)(n-k)k^2logk)$$, SC: $$O(k^2)$$
  * :thumbsup: Approach 2 - Sliding window
    * [Optimal Answer](https://leetcode.com/problems/minimum-absolute-difference-in-sliding-submatrix/submissions/2124302720). TC: $$O((m-k)(n-k)klogk)$$, SC: $$O(k^2)$$
