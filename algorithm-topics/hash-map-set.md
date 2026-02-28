---
description: Notes and typical questions for hash map or hash set related problems
icon: map-location-dot
---

# Hash Map/Set

## **Notes**

* If the array content is within a specific range, we can use `int[]` to replace `Map`
* If there are multiple `int[]` and you need to group them, you can convert `int[]` to `String` and use `String` as key in the `HashMap`
* If the result needs to be **deduped**, a 2/3 pointers solution may be easier to write with **sorting** the input array.
* Understanding HashMap Time Complexity
  * > A common question that always arises is: why are hashmap lookups considered $$O(1)$$ in terms of time complexity, even in worst-case scenarios? This seems counterintuitive, especially considering that hash collisions can occur.
    >
    > If we use a predetermined hash function, the worst-case time for hashmap operations could indeed be $$O(n)$$. Why? Because someone could craft a set of keys that all hash to the same value, causing a chain of collisions. This would force the lookup to scan through all $$n$$ elements, resulting in $$O(n)$$ time complexity.
    >
    > The key to achieving $$O(1)$$ time complexity lies in randomization. Instead of using a fixed hash function like `h(x) = (constant_a . x + constant_b) % constant_prime`, we can use a randomized approach. For example, we might choose random values for the parameters in our hash function each time we initialize our hashmap, such as `h(x) = (random_a . x + random_b) % random_prime`. (This is just one way to construct a hash function; there are many other types you can design.)
    >
    > This randomization makes it virtually impossible for someone to predict and exploit the hash function's behavior.
    >
    > From a mathematical perspective, when analyzing the "expected runtime" of hashmap operations using a randomized hash function, it averages out to $$O(1)$$. While some individual operations might take longer due to collisions, the overall average remains constant.
    >
    > It's crucial to understand that when we say "expected worst-case time is $$O(1)$$", we're referring to the average over all possible random choices of the hash function, for any given input.
    >
    > This isn't just theoretical—it’s applied in practice. For instance, Google’s Abseil library randomizes hash functions at the program start. This helps prevent attacks that exploit hash collisions and makes systems more secure. Randomization also ensures that software doesn't become dependent on a specific hash function. Hardcoding a hash function and never changing it makes future updates to improve security or performance challenging.
    >
    > This concept illustrates a broader principle in system design: the power of introducing controlled randomness to improve system performance and security. It also relates to Hyrum's Law, which suggests that all observable behaviors of a system will eventually be depended on by somebody. By randomizing hash functions, we prevent dependencies on specific hash behaviors, making systems more robust and flexible.
    >
    > Additionally, when we say "expected value," it's not just a random term; it is formally defined, similar to worst-case and average-case scenarios. You can read the definition and understand the concept here in [probability theory: Expected value](https://en.m.wikipedia.org/wiki/Expected_value).

## Typical Questions (28)

### Common Hash Map/Set Questions (22)

* LC 242. Valid Anagram
  * [Optimal Answer](https://leetcode.com/problems/valid-anagram/submissions/1784704548). TC: $$O(n)$$, SC: $$O(1)$$
* :orange\_circle: LC 49. Group Anagrams
  * Advanced version of LC 242, try to do it **without sorting**
  * [Optimal Answer](https://leetcode.com/problems/group-anagrams/submissions/1494752910). TC: $$O(n*m)$$_,_ SC: $$O(n*m)$$
* LC 349. Intersection of Two Arrays
  * [Optimal Answer](https://leetcode.com/problems/intersection-of-two-arrays/submissions/1389040917). TC: $$O(n)$$, SC: $$O(1)$$
* LC 454. 4Sum II
  * [Optimal Answer](https://leetcode.com/problems/4sum-ii/submissions/1690193975/). TC: $$O(n^2)$$, SC: $$O(n^2)$$
* LC 383. Ransom Note
  * [Optimal Answer](https://leetcode.com/problems/ransom-note/submissions/1784602856). TC: $$O(n)$$, SC: $$O(1)$$
* :white\_circle: LC 205. Isomorphic Strings
  * [Optimal Answer](https://leetcode.com/problems/isomorphic-strings/submissions/1784609176). TC: $$O(n)$$, SC: $$O(1)$$
* LC 290. Word Pattern
  * It's similar to above LC 205.
  * There is a single HashMap solution, but I still chose 2 HashMaps for better readability.
  * [Optimal Answer](https://leetcode.com/problems/word-pattern/submissions/1784659425).
    * $$N$$ represents the length of `s` and $$M$$ represents the length of `pattern`
    * TC: $$O(N+M)$$
    * SC: $$O(N)$$
* LC 438. Find All Anagrams in a String
  * This is actually a 2-pointer problem; my LC submission's time complexity is O(n)
* :star2: LC 15. 3Sum
  * Although "2 sum" can be solved by `HashMap`, this 3 sum is actually a 3-pointers problem; **it's hard to dedup results without sorting the input array**
  * Key point:&#x20;
    * Dedup result
    * Convert 3 sum to 2 sum variant (how many combinations to satisfy x+y==target?)
  * [Optimal Answer](https://leetcode.com/problems/3sum/submissions/1713921361/). TC: $$O(n^2)$$, SC: $$O(1)$$
* :white\_circle: LC 18. 4Sum
  * Similar to above LC 15. 3Sum
  * Be careful about the pruning operation using `break` inside the `for` loop. It is very error-prone.
  * [Optimal Answer](https://leetcode.com/problems/4sum/submissions/1713928215/). TC: $$O(n^3)$$, SC: $$O(1)$$
* :orange\_circle: LC 3404. Count Special Subsequences
  * This problem can be considered a more complex version of the '2 Sum' problem. In '2 Sum', we use a later element in the array to check if a corresponding earlier element exists in a hash map. Similarly, in this problem, we leverage later elements (`nums[s]/nums[r]`) to determine relationships with earlier elements (`nums[p]/nums[q]`)
  * [Optimal Answer](https://leetcode.com/problems/count-special-subsequences/submissions/1514140079). TC: $$O(n^2)$$, SC: $$O(n^2)$$
* LC 1679. Max Number of K-Sum Pairs
  * It's basically as same as 2 sum.
  * [Optimal Answer](https://leetcode.com/problems/max-number-of-k-sum-pairs/submissions/1463764360). TC: $$O(n)$$, SC: $$O(n)$$
* LC 2215. Find the Difference of Two Arrays
  * [Set Answer](https://leetcode.com/problems/find-the-difference-of-two-arrays/submissions/1464618903). TC: $$O(n)$$, SC: $$O(n)$$
  * [Map Answer](https://leetcode.com/problems/find-the-difference-of-two-arrays/submissions/1464617467). TC: $$O(n)$$, SC: $$O(n)$$
* LC 1207. Unique Number of Occurrences
  * [Optimal Answer](https://leetcode.com/problems/unique-number-of-occurrences/submissions/1464638593). TC: $$O(n)$$, SC: $$O(n)$$
* :white\_circle: LC 1657. Determine if Two Strings Are Close
  * It becomes straightforward once you realize this can be solved using `Map`. Be careful that `Set` cannot be used here and sort a constant array is $$O(1)$$ in TC!
  * [Optimal Answer](https://leetcode.com/problems/determine-if-two-strings-are-close/submissions/1465308385). TC: $$O(n)$$, SC: $$O(1)$$
* :orange\_circle: LC 2352. Equal Row and Column Pairs
  * To use an `int[]` as a key in a `Map`, convert the array to a `String` using `Arrays.toString(array)` and use the resulting `String` as the key.
  * [Optimal Answer](https://leetcode.com/problems/equal-row-and-column-pairs/submissions/1465352840). TC: $$O(n^2)$$, SC: $$O(n^2)$$
* :star2: :orange\_circle: LC 128. Longest Consecutive Sequence
  * It's hard to resolve it in $$O(n)$$. This brute force solution first.
  * 3 key points to get the optimal solution based on TC $$O(n^3)$$ brute force solution.
    * Use `Set` to do $$O(1)$$ look up.
    * Visited each sequence only once
      * Skip elements using this condition: `if (set.contains(num-1))` . In this case, we make sure we only visit the sequence when the current number can be the first number of this sequence.
      * Only using this condition still cannot guarantee we visit each sequence only once because the first number of this sequence can be duplicated in the input array. Therefore, we need to iterate `Set` instead of the input array to dedup.
  * [Optimal Solution](https://leetcode.com/problems/longest-consecutive-sequence/submissions/1485720447)
    * TC: $$O(n)$$. Although it looks like $$O(n^2)$$, it is actually $$O(n+n)$$. **Inner `while` loop only visits each element ONCE during the entire algorithm runtime.**
    * SC: $$O(n)$$
* LC 217. Contains Duplicate
  * [Optimal Answer](https://leetcode.com/problems/contains-duplicate/submissions/1486727811). TC: $$O(n)$$, SC: $$O(n)$$
* :white\_circle: LC 219. Contains Duplicate II
  * Try to resolve it using `Set` instead of `Map`
  * [Optimal Answer](https://leetcode.com/problems/contains-duplicate-ii/submissions/1541225883). TC: $$O(n)$$, SC: $$O(min(n,k))$$
* :white\_circle: LC 1930. Unique Length-3 Palindromic Subsequences
  * [Optimal Answer](https://leetcode.com/problems/unique-length-3-palindromic-subsequences/submissions/1533051214/?envType=company\&envId=google\&favoriteSlug=google-three-months). TC: $$O(n)$$, SC: $$O(1)$$
* LC 389. Find the Difference
  * [Optimal Answer](https://leetcode.com/problems/find-the-difference/submissions/1596986506). TC: $$O(n)$$, SC: $$O(1)$$
* LC 2043. Simple Bank System
  * [Optimal Answer](https://leetcode.com/problems/simple-bank-system/submissions/1895971427). For each method, TC: $$O(1)$$, SC: $$O(1)$$
* :white\_circle: LC 966. Vowel Spellchecker
  * [Optimal Answer](https://leetcode.com/problems/vowel-spellchecker/submissions/1896956364).&#x20;
  * Assume $$C$$ is the total _content_ of `wordlist` and `queries` .
    * TC: $$O(C)$$
    * SC: $$O(C)$$
* :white\_circle: LC 348. Design Tic-Tac-Toe
  * To achieve the optimal answer, always think about “What numeric quantity reaches an extreme when the answer happens?”
    * Try to express the win/answer condition as a **formula**, not a state.
    * Look for **sum / difference / count / max / min / parity**.
  * [Optimal Answer](https://leetcode.com/problems/design-tic-tac-toe/submissions/1911976445). TC: $$O(1)$$, SC: $$O(n)$$
* :white\_circle: LC 1169. Invalid Transactions
  * [Optimal Answer](https://leetcode.com/problems/invalid-transactions/submissions/1934087392). TC: $$O(n^2)$$, SC: $$O(n)$$

### **TreeMap/TreeSet (6)**

* Notes
  * Use cases
    * `TreeMap`is useful for maintaining a **dynamically sorted** collection of elements, especially when the **collection is frequently updated with new elements being added and old elements being removed**.
    * For each element in an array, `TreeMap` can be used for finding the following 2 requirements by adding array items to map from the end of the array.
      * the smallest element larger than the current element in elements after the current element
      * the largest element smaller than the current element in elements after the current element
* :orange\_circle: LC 1825. Finding MK Average
  * [Optimal Answer](https://leetcode.com/problems/finding-mk-average/submissions/1491003004)
    * `addElement(int num)`: TC $$O(log{n})$$, SC: $$O(n)$$, where $$n$$ is the number of unique elements in the map.
    * `calculateMKAverage()`: TC $$O(k)$$, SC $$O(1)$$
* :red\_circle: LC 975. Odd Even Jump
  * This solution is based on **DP + TreeMap** and this question can also be solved by **DP + Monotonic Stack**
  * [Optimal Solution](https://leetcode.com/problems/odd-even-jump/submissions/1492003113). TC: $$O(n*log{n})$$, SC: $$O(n)$$
* :red\_circle: LC 715. Range Module
  * This problem is super hard and has too many corner cases.
  * For a given range $$[left, right)$$ of add or remove action, we actually **ONLY** care about the interval that **overlaps with the left side** of the given range and the interval that **overlaps with the right side** of the given range. These 2 intervals could be the **same interval.**
  * [Optimal Solution](https://leetcode.com/problems/range-module/submissions/1506682729).
    * This solution is based on the comment of this [solution](https://leetcode.com/problems/range-module/solutions/108910/java-treemap/?envType=company\&envId=google\&favoriteSlug=google-three-months) in LC.
    * Let $$k$$ be the number of intervals to be cleared and $$N$$ be the size of the map.
    * TC:
      * `addRange` : $$O(k+logN)$$
      * `queryRange` :$$O(logN)$$
      * `removeRange` : $$O(k+logN)$$
    * SC: $$O(N)$$
* :white\_circle: LC 1146. Snapshot Array
  * [Optimal Answer](https://leetcode.com/problems/snapshot-array/submissions/1509083360).
    * `get()` and `set()`: $$O(logn)$$
    * `snap()`: $$O(1)$$
* LC 2349. Design a Number Container System
  * Another approach using Heap instead of TreeSet is also interesting.
  * [Optimal Answer](https://leetcode.com/problems/design-a-number-container-system/submissions/1538849443).
    * TC: `change(...)` is $$O(log{n})$$, `find(...)` is $$O(1)$$
    * SC: $$O(n)$$
* LC 681. Next Closest Time
  * [Optimal Answer](https://leetcode.com/problems/next-closest-time/submissions/1553137954/). TC: $$O(1)$$, SC: $$O(1)$$
* :orange\_circle: LC 2561. Rearranging Fruits
  * I initially misinterpreted the problem statement. After clarifying it, I solved most of the problem (\~90%), but I overlooked the crucial indirect swap case.
  * [Optimal Answer](https://leetcode.com/problems/rearranging-fruits/submissions/1884464160).&#x20;
    * Let n = `basket1.length` = `basket2.length`, and let k = number of distinct values across both baskets.
    * TC: $$O(n+k*logk)$$
    * SC: $$O(k)$$
* :orange\_circle: LC 1488. Avoid Flood in The City
  *   I only came up with a segment tree solution based on intuition because I initially modeled the problem as a **range query problem**. However, the real core operation is not “range sum”, but:

      > Find the smallest zero-day index strictly greater than `prev` (successor query).

      This is naturally solved by an ordered set (`TreeSet.higher(prev)`), so the segment tree was an over-generalized solution.
  * Approach 1 using Segment Tree:
    * [Answer](https://leetcode.com/problems/avoid-flood-in-the-city/submissions/1919420536). TC: $$O(n*(logn)^2)$$, SC: $$O(n)$$
  * Approach 2 using Improved Segment Tree:
    * [Optimal Answer](https://leetcode.com/problems/avoid-flood-in-the-city/submissions/1919437151). TC: $$O(n*logn)$$, SC: $$O(n)$$
  * :thumbsup: Approach 3 using Tree Set:
    * [Optimal Answer](https://leetcode.com/problems/avoid-flood-in-the-city/submissions/1919425763). TC: $$O(n*logn)$$, SC: $$O(n)$$

