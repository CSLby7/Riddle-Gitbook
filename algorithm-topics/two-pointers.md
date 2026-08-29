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

###
