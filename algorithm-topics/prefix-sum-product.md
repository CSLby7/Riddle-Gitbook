---
description: Notes and typical questions for prefix sum/product algorithm
icon: integral
---

# Prefix Sum/Product

## **Notes**

* Usually, prefix sum/product-related questions can be resolved within $$O(1)$$ space complexity.
* Use cases
  * When the problem is related to the sum of **subarrays**, prefix sum may be useful.

## **Typical Questions**

### **Classic Prefix Sum**

* LC 1480. Running Sum of 1d Array
  * [Optimal Answer](https://leetcode.com/problems/running-sum-of-1d-array/submissions/1496883382). TC: $$O(n)$$, SC: $$O(1)$$
* LC 1732. Find the Highest Altitude
  * [Optimal Answer](https://leetcode.com/problems/find-the-highest-altitude/submissions/1464590391). TC: $$O(n)$$, SC: $$O(1)$$
* :orange\_circle: LC 724. Find Pivot Index
  * It's kind of tricky to come up with the idea that is $$O(1)$$ in space.
  * [Optimal Answer](https://leetcode.com/problems/find-pivot-index/submissions/1464601243). TC: $$O(n)$$, **SC:** $$O(1)$$
*   :white\_circle: LC 238. Product of Array Except Self

    * The implementation is a bit tricky if resolving it by $$O(1)$$ in space. Since `result[i] = prefix[i-1] * suffix[i+1]`, we can adjust the prefix and suffix arrays to **align their values accordingly** to make code more elegant.&#x20;
    * [Optimal Answer](https://leetcode.com/problems/product-of-array-except-self/submissions/1462979079). TC: $$O(n)$$, **SC:** $$O(1)$$

    <figure><img src="../.gitbook/assets/LC-238 (1).svg" alt=""><figcaption></figcaption></figure>
* :star2: :orange\_circle: LC 560. Subarray Sum Equals K
  *   At first glance, I thought this was a two-pointer problem, **but it's NOT**, for the following reasons:

      > Because prefixSum can either increase or decrease towards the forward movement due to the presence of negative values in the array. Sliding window is only applicable when we know for sure if the prefixSum is an increasing or decreasing function.
  * This problem solution equals to prefix sum + 2 sum approach.
  * [Optimal Solution](https://leetcode.com/problems/subarray-sum-equals-k/submissions/1494573680). TC: $$O(n)$$, SC: $$O(1)$$
* :orange\_circle: LC 152. Maximum Product Subarray
  * The optimal answer is genius...
  * [Optimal Answer](https://leetcode.com/problems/maximum-product-subarray/submissions/1564464836). TC: $$O(n)$$, SC: $$O(1)$$
    * > First, if there's no zero in the array, then the subarray with maximum product must start with the first element or end with the last element. And therefore, the maximum product must be some prefix product or suffix product. So in this solution, we compute the prefix product `A` and suffix product `B`, and simply return the maximum of `A` and `B`.
      >
      > Why? Here's the proof:
      >
      > Say, we have a subarray `A[i : j]`(`i != 0`, `j != n`) and the product of elements inside is `P`. Take `P > 0` for example: if `A[i] > 0` or `A[j] > 0`, then obviously, we should extend this subarray to include `A[i]` or `A[j]`; if both `A[i]` and `A[j]` are negative, then extending this subarray to include both `A[i]` and `A[j]` to get a larger product. Repeating this procedure and eventually we will reach the beginning or the end of `A`.
      >
      > What if there are zeroes in the array? Well, we can split the array into several smaller ones. That's to say, when the prefix product is `0`, we start over and compute prefix profuct from the current element instead. And this is exactly what `A[i] *= (A[i - 1]) or 1` does.

### **Difference Array (Sweep Line Algo)**

* Notes:
  * It is a type of range update and prefix sum algorithm used for efficiently applying multiple range updates and querying cumulative results.
  * Use cases
    * Range Updates: For problems involving range updates and queries, such as Incrementing or decrementing values in a range. Setting or modifying values in a range.
    * Counting Problems: To efficiently count occurrences or compute cumulative data over ranges.
  * References: [https://codeforces.com/blog/entry/78762](https://codeforces.com/blog/entry/78762)
* :star2: :orange\_circle: LC 3355. Zero Array Transformation I
  * [Optimal Answer](https://leetcode.com/problems/zero-array-transformation-i/submissions/1473820963). TC: $$O(n)$$, SC: $$O(n)$$
* :red\_circle: LC 3356. LC Zero Array Transformation II
  * Idea
    * It's kind of a greedy idea as well. Only apply the next query when the current `nums[i]` is not zero based on previously used queries.
    * We cannot pre-calculate the difference array first because we need to know how many queries are used when handling `nums[i]`. Therefore, we need to combine all logic together into 1 for loop and do everything (use query, update difference array, update cumulative sum, record how many queries are used) in parallel at the same time.
  * [Optimal Answer](https://leetcode.com/problems/zero-array-transformation-ii/submissions/1473848010). TC: $$O(n)$$, SC: $$O(n)$$
* :red\_circle: LC 3362. Zero Array Transformation III
  * This solution is very ingenious and difficult to come up with; it skillfully combines the greedy algorithm with the difference array algorithm.
  * [Optimal Answer](https://leetcode.com/problems/zero-array-transformation-iii/submissions/1536208502). TC: $$O(n+q*log{q})$$, SC: $$O(n)$$
* :orange\_circle: LC 1381. Design a Stack With Increment Operation
  * Try to resolve it using the array data structure without any stack data structure.
  * [Optimal Answer](https://leetcode.com/problems/design-a-stack-with-increment-operation/submissions/1568451919/). TC: $$O(1)$$, SC: $$O(n)$$

### **Probability**

* LC 528. Random Pick with Weight
  * Constructor: TC $$O(N)$$, SC $$O(N)$$
  * `pickIndex()`: TC $$O(log{N})$$, SC $$O(1)$$

### Simulation

* :white\_circle: LC 3494. Find the Minimum Amount of Time to Brew Potions
  * My [original answer](https://leetcode.com/problems/find-the-minimum-amount-of-time-to-brew-potions/submissions/1593791521) can be simplified in terms of implementation (do not need to keep updating the prefix sum array).
  * [Optimal Answer](https://leetcode.com/problems/find-the-minimum-amount-of-time-to-brew-potions/submissions/1593793793). TC: $$O(m*n)$$, SC: $$O(n)$$
