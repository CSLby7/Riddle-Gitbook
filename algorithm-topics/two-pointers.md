---
description: Notes and typical questions for two pointers algorithm
icon: right-left
---

# Two Pointers

## **Notes**

* Check if the question requires manipulating the array **in place**. If not, maybe having a new array can resolve it quickly.

## Typical Questions

### Other 2 Pointers Problems

* LC 977. Squares of a Sorted Array
* :red\_circle: LC 76. Minimum Window Substring
* LC 438. Find All Anagrams in a String
  * This is also listed under HashMap, my LC submission's time complexity is O(n)
* :star2: :red\_circle: LC 962. Maximum Width Ramp
  * This problem can also be resolved by monotonic stack (see that section)
  * [Optimal Solution](https://leetcode.com/problems/maximum-width-ramp/submissions/1491044381). TC: $$O(n)$$, SC: $$O(n)$$
* :star2: :red\_circle: LC 2863. Maximum Length of Semi-Decreasing Subarrays
  * This question is the same as LC 962
  * Approach 1: Monotonix Stack. TC: $$O(n)$$, SC: $$O(n)$$
  * Approach 2: 2 pointers + `rightMin` array. TC: $$O(n)$$, SC: $$O(n)$$
* :white\_circle: LC 696. Count Binary Substrings
  * [Optimal Answer](https://leetcode.com/problems/count-binary-substrings/submissions/1941557061). TC: $$O(n)$$, SC: $$O(1)$$
* LC 244. Shortest Word Distance II
  * [Optimal Answer](https://leetcode.com/problems/shortest-word-distance-ii/submissions/1988037362).&#x20;
  * TC: Constructor $$O(n)$$, `shortest`: $$O(k1+k2)$$
  * SC: $$O(n)$$
  * Follow-ups when wordDict is big or certain words have a higher frequency
    * Add cache
    * If the two words’ index lists have very different sizes, iterate through the smaller list and binary search in the larger list for the closest index. TC: $$O(min(k1, k2)*log(max(k1, k2)))$$
* LC 360. Sort Transformed Array
  * [Optimal Answer](https://leetcode.com/problems/sort-transformed-array/submissions/1994469685). TC: $$O(n)$$, SC: $$O(1)$$

### Strings Match

* LC 392. Is Subsequence
  * Method 1: 2 pointers. Its **performance is better DP** and it's super easy to implement;
    * [Optimal Answer](https://leetcode.com/problems/is-subsequence/submissions/1463718029). TC: $$O(n)$$, SC: $$O(1)$$
  * :orange\_circle: Method 2: DP. Need to realize it's very similar to LC 1143...
* :white\_circle: LC 2337. Move Pieces to Obtain a String
  * [Optimal Answer](https://leetcode.com/problems/move-pieces-to-obtain-a-string/submissions/1513973674). TC: $$O(n)$$, SC; $$O(1)$$
* :white\_circle: LC 408. Valid Word Abbreviation
  * [Optimal Answer](https://leetcode.com/problems/valid-word-abbreviation/submissions/1880068947/). TC: $$O(n)$$, SC: $$O(1)$$

### N Sum Problems

* LC 167. Two Sum II - Input Array Is Sorted
  * It's the foundation of LC 15. 3Sum
  * [Optimal Answer](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/submissions/1778291056). TC: $$O(n)$$, SC: $$O(1)$$
* :star2: LC 15. 3Sum
  * Although "2 sum" can be solved by `HashMap`, this 3 sum is actually a 3 pointers problem, **it's hard to dedup result without sorting input array**
* LC 16. 3Sum Closest
  * It's similar to LC 15 and easier than it.
  * [Optimal Answer](https://leetcode.com/problems/3sum-closest/submissions/1492794642). TC: $$O(n^2)$$, SC: $$O(1)$$
* LC 1925. Count Square Sum Triples
  * [Optimal Answer](https://leetcode.com/problems/count-square-sum-triples/submissions/1964465799). TC: $$O(n^2)$$, SC: $$O(1)$$
*   LC 11. Container With Most Water

    * This is a two-pointer problem (variant of LC 167), but it is easily mistaken for a monotonic stack solution.
    * [Optimal Answer](https://leetcode.com/problems/container-with-most-water/submissions/1463752284). TC: $$O(n)$$, SC: $$O(1)$$

    > The widest container (using first and last line) is a good candidate, because of its width. Its water level is the height of the smaller one of first and last line. All other containers are less wide and thus would need a higher water level in order to hold more water. The smaller one of first and last line doesn't support a higher water level and can thus be safely removed from further consideration. if h\[i], h\[j], where h\[i]==h\[j], are at maximum width, then for any other pair of heights with narrower width, the min height would need to be taller than both h\[i] and h\[j]. So NEITHER i or j is a valid contender for future maximums at a narrower widthand you can actually increment/decrement both. You can change the code to check for equal heights and do i++ and j-- and verify.

### **Merge Elements**

* :white\_circle: LC 88. Merge Sorted Array
  * It’s easy to overlook that the for loop can be **exited early**.
  * [Optimal Answer](https://leetcode.com/problems/merge-sorted-array/submissions/1473979015). TC: $$O(m+n)$$, SC: $$O(1)$$
* :white\_circle: LC 1570. Dot Product of Two Sparse Vectors
  * [Optimal Answer](https://leetcode.com/problems/dot-product-of-two-sparse-vectors/submissions/1975054684).&#x20;
  * Let $$n$$ be the length of the input array and $$L$$ be the number of non-zero elements for the vector.
  * TC: $$O(n)$$, SC: $$O(L)$$

### **Delete/Overwrite Elements**

* Notes
  * Fast and slow pointers are useful for questions related to **moving/removing** items in an array. The fast pointer is used for exploring the array. The slow pointer is used to point to the index that can store value when the fast pointer points to the expected value.
  * For moving element, consider it in 2 ways: moving target value or moving items that are not target values
  * Check if the question requires keeping the array in the same order at the end
  * When swapping f/s pointer items, always introduce **temp value** to avoid exceptions in corner cases (LC 283)
* LC 26. Remove Duplicates from Sorted Array
  * [Optimal Answer.](https://leetcode.com/problems/remove-duplicates-from-sorted-array/submissions/1854930065) TC: $$O(n)$$, SC: $$O(1)$$
* :white\_circle: LC 80. Remove Duplicates from Sorted Array II
  * It's easy to miss a corner case (if you just compare `nums[f]` and `nums[f-2]`)
  * The optimal solution is more logical than the solution I came up with by myself (although TC and SC are the same)
  * [Optimal Answer](https://leetcode.com/problems/remove-duplicates-from-sorted-array-ii/submissions/1764496334). TC: $$O(n)$$, SC: $$O(1)$$
* LC 27. Remove Element
* LC 443. String Compression
  * [Optimal Answer](https://leetcode.com/problems/string-compression/submissions/1463709973). TC: $$O(n)$$, SC: $$O(1)$$
* :white\_circle: LC 283. Move Zeroes
  * [Optimal Answer](https://leetcode.com/problems/move-zeroes/submissions/1377117429). TC: $$O(n)$$, SC: $$O(1)$$
* LC 2390. Removing Stars From a String
  * Stack approach: Use `StringBuilder` to simulate `Stack`. [Answer](https://leetcode.com/problems/removing-stars-from-a-string/submissions/1465358090). TC: $$O(n)$$, SC: $$O(n)$$
  * 2 pointers approach: [Answer](https://leetcode.com/problems/removing-stars-from-a-string/submissions/1465361947). TC: $$O(n)$$, SC: $$pseudo-O(1)$$ due to the immutability of `String` in Java

### **Sliding Window - General**

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

### **Sliding Window - Subarray/Substring Search Meeting With Requirements**

#### Notes

* Two-pointers are also useful when you need to **explore a set of subarrays/substrings that meet certain conditions** in a given input array/string and calculate results while exploring subarrays. For this kind of question, you usually need to use a fast point to explore the array and move the left pointer when the subarray does not meet the condition.

#### :jigsaw: **Sliding Window with Aggressive Shrinking**

* Notes
  * You may need to use **`while` loop to move the left pointer until the subarray meets the condition**.
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
  * 2 cases for central point (the value that elements get updated to)
    * It's an existing element
      * **After sorting, for each element `e` in the array, there is a technique to find the number of elements within the range `[e-k,e+k]` in** $$O(n)$$ **by scanning the array once.**
    * It's a value that does not exist in the input array
  * [Optimal Answer](https://leetcode.com/problems/maximum-frequency-of-an-element-after-performing-operations-i/submissions/1515093798). TC: $$O(n*log{n})$$, SC: $$O(n)$$
* :white\_circle: LC 2762. Continuous Subarrays
  * There is another optimal answer that only uses 2 pointers without `TreeMap` . Since it has the same TC and SC as my answer and it's more complicated to understand, I did not use it.
  * [Optimal Answer](https://leetcode.com/problems/continuous-subarrays/submissions/1562157563).
    * Let $$n$$ be the size of input, and $$k$$ be the size of `TreeMap` . Since $$k$$ should always <= 3 based on the requirement of the question, we can treat $$k$$ as a constant
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

#### :jigsaw: **Sliding Window with Non-Aggressive Shrinking**

* Notes
  * You may **NOT use `while` loop to move the left pointer until the subarray meets the condition** and **NOT shrink the window below the max window size found previously**.
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
      * That's also why we do **NOT need to consider decreasing `maxFreq`** when moving `start` index and do **NOT care if it is stale**. We **ONLY care and want to find a larger `maxFreq`**
