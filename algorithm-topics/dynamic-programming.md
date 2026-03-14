---
description: Notes and typical questions for dynamic programming algorithm
icon: diagram-successor
---

# Dynamic Programming

## **Notes**

* Steps to resolve the problem
  1. Define the meaning of the DP array (dp table) and its indices
  2. Determine the recurrence formula
  3. Initialize the DP array
  4. Define the traversal order
  5. Use an example to derive the DP array

## **Typical Questions**

### **Miscellaneous DP**

* LC 509. Fibonacci Number
* LC 1137. N-th Tribonacci Number
  * [Optimal Answer](https://leetcode.com/problems/n-th-tribonacci-number/submissions/1470486362). TC: $$O(n)$$, SC: $$O(1)$$
* LC 118. Pascal's Triangle
  * [Optimal Answer](https://leetcode.com/problems/pascals-triangle/submissions/1498109080). TC: $$O(numRows^2)$$, SC: $$O(1)$$ (without considering space for storing the result)
* LC 70. Climbing Stairs
* LC 746. Min Cost Climbing Stairs
  * [Optimal Answer](https://leetcode.com/problems/min-cost-climbing-stairs/submissions/1442036198). TC: $$O(n)$$, SC: $$O(1)$$
* :red\_circle: LC 790. Domino and Tromino Tiling
  * TBH, it's very hard. I will forget how to solve it next time.
  * [Answer](https://leetcode.com/problems/domino-and-tromino-tiling/submissions/1470524453). This answer is not optimal, but more readable. TC: $$O(n)$$, SC: $$O(n)$$
*   LC 343. Integer Break

    * :orange\_circle: Method 1: DP
      * [Answer](https://leetcode.com/problems/integer-break/submissions/1755123983/). TC: $$O(n^2)$$, SC: $$O(n)$$
    * :red\_circle: Method 2: Math

    ```java
    // 把一个正整数拆成若干个正整数，使其拆分后的数乘积最大，
    // 假设 N = n1 + n2 + ... + nk;

    // 1. 显然，1 不在n1...nk中
    // 2. 如果对于某 i 有 ni >= 5, 那么把 ni 拆成 3+(ni-3), 我们有3(ni-3) = 3ni -9 > ni, 所以不存在>=5的因子
    // 3. 如果 ni = 4, 拆成 2+2, 乘积不变，所以不妨假设没有4
    // 4. 如果拆成三个以上的2，那么 3*3 > 2*2*2，所有替换成3乘积最大, 不可能有>=3个2
    // 综上，选用尽量多的3，直到剩下2或者4时用2.

    if (n == 2) return 1;
    if (n == 3) return 2;
    int num_3 = (int)n/3;
    int remainder = n % 3;
    if (remainder == 1) {
        remainder = 4;
        num_3 --;
    } else if (remainder == 0) 
        remainder = 1;

    return (int)Math.pow(3, num_3) * remainder;
    ```
* :white\_circle: LC 96. Unique Binary Search Trees
  * [DP Answer](https://leetcode.com/problems/unique-binary-search-trees/submissions/1755169933/). TC: $$O(n^2)$$, SC: $$O(n)$$
* :red\_circle: LC 312. Burst Balloons
  * It's super hard to come up with the correct idea
  * [Optimal Solution](https://leetcode.com/problems/burst-balloons/submissions/1487487712). TC: $$O(n^3)$$, SC: $$O(n^2)$$
* :red\_circle: LC 3351. Sum of Good Subsequences
  * Use both `long`and module operation to avoid overflow.
  * [Optimal Answer](https://leetcode.com/problems/sum-of-good-subsequences/submissions/1520538051). TC: $$O(n)$$, SC: $$O(n)$$
* :red\_circle: LC 2184. Number of Ways to Build Sturdy Brick Wall
  * It's very complicated:  DP + Backtracking + Bit
  * [Optimal Answer](https://leetcode.com/problems/number-of-ways-to-build-sturdy-brick-wall/submissions/1544309247/).
    * Assume $$B$$ is the number of brick sizes, $$H$$ and $$W$$ are the height and width of the wall, $$N$$ is the number of ways to build 1 row
    * TC: $$B^{W}+H*N^{2}$$
    * SC: $$N^{2}+H*H$$
* :red\_circle: LC 3287. Find the Maximum Sequence Value of Array
  * [Optimal Answer](https://leetcode.com/problems/find-the-maximum-sequence-value-of-array/submissions/1552076940/). TC: $$O(n*k)$$, SC: $$O(n*k)$$
* :orange\_circle: LC 2327. Number of People Aware of a Secret
  * I came up with an n^2 solution, but that's not good enough.
  * The definition of this dp array and how to do state transition is tricky.
  * [Optimal Answer](https://leetcode.com/problems/number-of-people-aware-of-a-secret/submissions/1914353991). TC: $$O(n)$$, SC: $$O(n)$$

### Pattern Counting

* Notes
  * Group configurations into a few pattern types instead of enumerating all possibilities.
  * Let each pattern type be a DP state representing how many ways it can appear.
* :orange\_circle: LC 1411. Number of Ways to Paint N × 3 Grid
  * [Optimal Answer](https://leetcode.com/problems/number-of-ways-to-paint-n-3-grid/submissions/1943508321). TC: $$O(n)$$, SC: $$O(1)$$

### 2D Matrix Problems

* LC 62. Unique Paths
  * [Optimal Answer](https://leetcode.com/problems/unique-paths/submissions/1470562774). TC: $$O(m*n)$$, SC: $$O(n)$$
* LC 63. Unique Paths II
  * [Optimal Answer](https://leetcode.com/problems/unique-paths-ii/submissions/1754396403/). TC: $$O(m*n)$$, SC:  $$O(1)$$. This approach modifies input data so it's. kind of hacky.
  * [Answer](https://leetcode.com/problems/unique-paths-ii/submissions/1442041350/). TC: $$O(m*n)$$, SC:  $$O(n)$$.&#x20;
* LC 221. Maximal Square
  * [Optimal Solution](https://leetcode.com/problems/maximal-square/submissions/1506736565). TC: $$O(m*n)$$, SC: $$O(1)$$
* :red\_circle: LC 2713. Maximum Strictly Increasing Cells in a Matrix
  * It's very hard to come up with this solution.
  * For each point, a separate data structure must be used to help find the current max step in its column and row.
    * Optimal Solution. TC: $$O(n*m*log{nm})$$,  SC: $$O(n*m)$$
* LC 120. Triangle
  * [Optimal Answer](https://leetcode.com/problems/triangle/submissions/1877016028). TC: $$O(n^2)$$, SC: $$O(n)$$
* LC 64. Minimum Path Sum
  * [Optimal Answer](https://leetcode.com/problems/minimum-path-sum/submissions/1877128709). TC: $$O(m*n)$$, SC: $$O(n)$$
* :red\_circle: LC 808. Soup Servings
  * This DP problem requires some techniques I never seen before.
  * Core Idea
    * How to address stack overflow or TLE if using backtracking?
      * Use DP
    * What's the base case of DP?
    * How to address Memory Limit Exceeded when the DP table is too big?
      * Based on the law of large numbers, we don't have to calculate every case when the input is too big because the problem mentions that answers within 1e-5 are accepted.
    * What's the traversal order if we may not want to calculate every case
      * Not line by line or column by column. We should go from (i, i) to (i+1,i+1)
  * [Optimal Answer](https://leetcode.com/problems/soup-servings/submissions/1889464716). TC: $$O(1)$$, SC: $$O(1)$$

### **Knapsack Problems**

#### :jigsaw: **0-1 Knapsack Problem**

* Notes
  * Assumption: Each item can only be used once to fill a knapsack of size k.
  * Kinds of problems
    * The maximum value to fill the knapsack <-> Whether it is possible to fill a knapsack of size k
    * The number of ways to fill a knapsack of size k **(be careful about initialization)**
    * The max/min number of items to fill the knapsack of size k
* :star2: :red\_circle: LG P1048 \[NOIP2005 普及组] 采药
  * Be careful when using 1D array: inner loop iteration order & size of 1D array & inner loop termination logic
* LC 416. Partition Equal Subset Sum
  * [Optimal Answer](https://leetcode.com/problems/partition-equal-subset-sum/submissions/1755270921/). TC: $$O(n*target)$$, SC: $$O(target)$$
* LC 1049. Last Stone Weight II
  *   [Optimal Answer](https://leetcode.com/problems/last-stone-weight-ii/submissions/1182566944/). TC: $$O(n*target)$$, SC: $$O(target)$$

      > 为什么两两单个相撞可以等效于两个group相撞： 整个题目，每个回合数两两抽出来比较，两个数之差将被再一次扔到数组里面，继续上面的过程。每个回合都会丢失掉两个数字，加入一个新的数字，这个数字就是两个数的差。相当于来说，就是少了a和b，但是多了一个a-b，a,b就此消失，但是在下一回合，a-b可能又被抓出去pk，pk后a-b就此再消失了，又产生了新的一个差。那么每一步来说，其实就相当于a,b没有真正意义消失。 到了最后一回合，我们可以知道，其实找出两个最接近的数字堆。 再举个例子：【31,26,33,21,40】 1:40-21 【19,26,31,33】 2: 31-(40-21) 【12,26,33】 3: 33-(31-(40-21)) 【21,26】 4: 26-(33-(31-(40-21))) 【5】 总： （26+31+21） - （40+33） 这就是找出两个总和接近的两个堆。 如何让两个堆接近呢？ 那就是沿着中间分两半，找左右各自那一半，那么思路就来到了找出一半堆这里。那么就自然而然地来到取不取的问题，就是01背包问题。
* :red\_circle: LC 494. Target Sum
  * [Optimal Answer](https://leetcode.com/problems/target-sum/submissions/1444429132/). TC: $$O(n*part1)$$, SC: $$O(part1)$$
* :orange\_circle: LC 474. Ones and Zeroes
  * [Optimal Answer](https://leetcode.com/problems/ones-and-zeroes/submissions/1445340746/). TC:  $$O(l*m*n)$$, SC: $$O(m*n)$$
* :star2: :red\_circle: 1235. Maximum Profit in Job Scheduling
  * I came up with the main idea by myself, but my original answer failed due to "Memory Limit Exceeded". The gap is that I did not find a way to compress the DP array from (0, maxEndTime) to (0, number of unique jobEndTimes).
  * Both answers below are optimal. TC: $$O(n*logn)$$, SC: $$O(n)$$
    * [DP + TreeMap Answer](https://leetcode.com/problems/maximum-profit-in-job-scheduling/submissions/1598881158).
    * [DP + Binary Search Answer](https://leetcode.com/problems/maximum-profit-in-job-scheduling/submissions/1598894708). While it has the same TC as the TreeMap answer, it is faster based on the LC evaluation.

#### :jigsaw: **Complete Knapsack Problem**

* Notes
  * Assumption: Each item can only be used multiple times to fill a knapsack of size k.
  * Kinds of problems
    * The maximum value to fill the knapsack
    * The number of ways to fill a knapsack of size k (be careful about initialization)
    * The max/min number of items to fill the knapsack of size k
  * The **ORDER** of the **INNER** and **OUTER loop**
    * High level speaking, 对于纯粹的完全背包，是否能调换两层循环（物品，重量）？从结果角度，可以。从过程角度，如果先循环重量，再循环物品，中间有些dp\[i]的含义会有问题，会超前使用某些之前的值做推断，但不影响结果。可用 w: (1,2,3,4), v: (10, 21, 33, 44),分别写两种方法的dp表格。对于完全背包的相关应用，内外循环不一定能调换。
    * Low-level speaking
      * Outer loop for items & inner loop for weights -> get the result from all **combinations**
      * Outer loop for weights & inner loop for items -> get the result from all **permutations**
* :star2: :red\_circle: LG P1616 疯狂的采药
* LC 518. Coin Change II
  * Looks like a backtracking problem but it's easier to solve it using DP.
  * [Optimal Answer](https://leetcode.com/problems/coin-change-ii/submissions/1756486861/). TC: $$O(n*amount)$$, SC: $$O(amount)$$
  *   This is a combination problem. Its iteration must be "outer loop for items & inner loop for weights". If you do it in reverse way, you will get a permutation result.

      > 对于外层遍历物品的时候，对于每一个物品比如物品1，内层是在不断地遍历背包容量，这个物品可以被重复地添加进来，当外层遍历到下一个物品2的时候，内层又会不断地遍历背包容量，这个物品也可以被重复地添加进来，但是这个物品2一定是在物品1后面的，不会出现物品2 物品1这种情况，所以是没有考虑到物品的顺序的，所以是组合 如果外层遍历背包，内层物品，那么对于每一个背包容量，都会把所有物品遍历一次，虽然在本次外层循环中，物品2会在物品1之后，但是下一个外层循环的时候，又会遍历所有物品，整体看起来就会出现 物品1 物品2 物品1这种情况了，所以是排列问题。
* LC 377. Combination Sum IV
  * It's actually a _**permutation**_ problem...It's very similar to LC 518. Coin Change II and the only difference is its requirement on the order of the result.
  * 70\. Climbing Stairs problem can be abstracted to this problem as well. However, compared to thinking about it in a complete knapsack way, the original idea is better.
  * [Optimal Answer](https://leetcode.com/problems/combination-sum-iv/submissions/1756496288/). TC: $$O(n*target)$$, SC: $$O(target)$$
* :star2: :white\_circle: LC 322. Coin Change
  * [Optimal Answer](https://leetcode.com/problems/coin-change/submissions/1448975188). TC: $$O(n*amount)$$, SC: $$O(amount)$$
* LC 279. Perfect Squares
  * It's the same as the above one.
  * [Optimal Answer](https://leetcode.com/problems/perfect-squares/submissions/1448977760/). TC: $$O(n*\sqrt{n})$$$$O(n*$sqrt{n}$)$$, SC: $$O(n)$$
* :orange\_circle: LC 139. Word Break
  * This question is also put in the Trie section.
  * Given $$n$$ as the length of `s`, $$m$$ as the length of `wordDict`, and $$k$$ as the average length of the words in `wordDict`
    * [Straightforward DP Answer](https://leetcode.com/problems/word-break/submissions/1448983585).&#x20;
      * TC: $$O(n^3 + m*k)$$
      * SC: $$O(n+m*k)$$
    * :thumbsup: [Optimal Answer](https://leetcode.com/problems/word-break/submissions/1505502045) (DP+Trie).
      * The idea of doing dp is different from the above straightforward one.
      * TC: $$O(n^2+m*k)$$
      * SC: $$O(n+m*k)$$
    * :thumbsup: [Knapsack Answer](https://leetcode.com/problems/word-break/submissions/1757746212/).
      * TC: $$O(n*m*k)$$
      * SC: $$O(n)$$

### **House Robber**

* :star2: LC 198. House Robber
  * [Optimal Answer](https://leetcode.com/problems/house-robber/submissions/1450163082). TC: $$O(n)$$, SC: $$O(1)$$
* :star2: :white\_circle: LC 213. House Robber II
  * **Transform a circular problem into a linear one using case-by-case analysis.** (case1: exclude 1st item, case2: exclude last item)
  * [Optimal Answer](https://leetcode.com/problems/house-robber-ii/submissions/1268959405/).  TC: $$O(n)$$, SC: $$O(1)$$
* :orange\_circle: LC 337. House Robber III
  * Tree DP. I have most of the main idea, but it's easy to make mistakes in the case where the current node is not being robbed.
  * [Optimal Answer](https://leetcode.com/problems/house-robber-iii/submissions/1453965715/). TC: $$O(n)$$, SC: $$O(h)$$
* :white\_circle: LC 3186. Maximum Total Damage With Spell Casting
  * House Robber Variant: conflict defined by value distance instead of index adjacency. Need to find the last compatible state.
  * TC: $$O(nlogn)$$, SC: $$O(n)$$

### :jigsaw: **Stock Problems**

* Notes
  * General assumptions
    * You can only hold at most 1 share of stock at any time
    * Must sell the stock before you buy again
    * **Transaction times `k`** (most important assumption)
      * if no requirement on `k`, then 2 states for stocks (hold or not hold)
      * if `k == i` (`i` is an input constant), then `2*k` state for stocks
        * For example, if `k == 2`, states: s0 -> 1st hold, s1 -> 1st not hold, s2 -> 2nd hold, s3 -> 2nd not hold
    * Have a cooldown day or not (easy to add this logic)
    * Have transaction fee or not (easy to add this logic)
  * Key: Define stock holding status, usually defined as `dp[i][s]`, i -> ith day, s -> all states based on assumption
* :star2: :orange\_circle: LC 121. Best Time to Buy and Sell Stock
  * Alternative greedy algo answer: For each `prices[i]`, find the min value which is on the left (including the current one), and keep updating `result`.
  * DP answer can be improved to a 1D DP array.
  * Approach 1 with DP: [Optimal Answer](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/submissions/1475593321/). TC: $$O(n)$$, SC: $$O(1)$$
  * Approach 2 with brute force: [Optimal Answer](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/submissions/1765513935). TC: $$O(n)$$, SC: $$O(1)$$
* LC 122. Best Time to Buy and Sell Stock II
  * Alternative greedy algo answer: Accumulate positive revenue and keep updating results.
  * DP answer can be improved to a 1D DP array with `tmp` var.
  * [Optimal Answer](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/submissions/1454618479/). TC: $$O(n)$$, SC: $$O(1)$$
    * 也可以不用`tmp`, 相当于允许当天买入+卖出的操作。
* :star2: :orange\_circle: LC 123. Best Time to Buy and Sell Stock III
  * [Optimal Answer](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iii/submissions/1454673418/). TC: $$O(n)$$, SC: $$O(1)$$
  * 也可以把for循环里面的顺序正过来，原因如下
  * > 大家会发现dp\[1]利用的是当天的dp\[0]。 但结果也是对的。
    >
    > 我来简单解释一下：
    >
    > `dp[0] = max(dp[0], -prices[i]);`
    >
    > * 如果`dp[0]` 取 `dp[0]`，即保持买入股票的状态，那么 `dp[1] = max(dp[1], dp[0] + prices[i]);` 中 `dp[0] + prices[i]` 就是今天卖出。
    > * &#x20;如果`dp[0]` 取 `-prices[i]`，今天买入股票，那么 `dp[1] = max(dp[1], dp[0] + prices[i]);` 中 `dp[1] + prices[i]` 相当于是今天再卖出股票，一买一卖收益为0，对所得现金没有影响。相当于今天买入股票又卖出股票，等于没有操作，保持昨天卖出股票的状态了。
* LC 188. Best Time to Buy and Sell Stock IV
  * Similar to LC 123
  * [Optimal Answer](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iv/submissions/1760949412/). TC: $$O(n*k)$$, SC: $$O(k)$$
* :orange\_circle: LC 309. Best Time to Buy and Sell Stock with Cooldown
  * Approach 1 with  2 states: [Answer](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-cooldown/submissions/1760961584/).  TC: $$O(n)$$, SC: $$O(n)$$. Not easy to compress its SC.
  * :thumbsup: Approach 2 with 3 states: [Optimal Answer](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-cooldown/submissions/1760967541/). TC: $$O(n)$$, SC: $$O(1)$$
* LC 714. Best Time to Buy and Sell Stock with Transaction Fee
  * [Optimal Answer](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-transaction-fee/submissions/1470574349). TC: $$O(n)$$, SC: $$O(1)$$.

### **Subsequence/Subarray Problems**

* Notes
  * Difference
    * subsequence: order matters, can skip element
    * substring: order matters, must consecutive
  * For subsequence problems, think about "If I pick an element, what info about the past do I need to know to decide if I can append it?"
    * That info becomes your DP state.
      * If it’s just the last value → `dp[last]`
      * If it’s last two-ish pattern → `dp[a][b]` (like LC3202)
      * If it’s last value + budget → `dp[last][used]`&#x20;
        * The “budget” can be _anything constrained_:
          * number of changes
          * number of mismatches
          * number of deletions
          * number of replacements
          * number of violations
          * number of operations

#### :jigsaw: **Classic Subsequence/Subarray**

* :star2: LC 300. Longest Increasing Subsequence
  * Approach 1: Classic DP
    * `dp[i]`: longest increasing subsequence **including nums\[i]**
    * [Answer](https://leetcode.com/problems/longest-increasing-subsequence/submissions/1280001356/). TC: $$O(n^2)$$, SC: $$O(n)$$
  * :thumbsup: :red\_circle: Approach 2: **Intelligently Build a Subsequence + Binary Search**
    * This approach is hard to understand. I feel like its core logic/concept (keep exploring the array though elements within the array are not always valid) is similar to another 2-pointer question.&#x20;
    * > While **the content of sub might not be an actual subsequence from nums**, its length corresponds to the length of the LIS. This is because every time we append a number to sub, it means we have found a longer increasing sequence than any we have seen before. When we replace an element in sub, we're not extending the length of the sequence, but we are making the increasing sequence that we can potentially build later more flexible (i.e., able to accommodate smaller subsequent numbers).
    * [Optimal Answer](https://leetcode.com/problems/longest-increasing-subsequence/submissions/1511884792/). TC: $$O(n*log{n})$$, SC: $$O(n)$$
  * :red\_circle: Approach 3: Segment Tree
    * [Answer](https://leetcode.com/problems/longest-increasing-subsequence/submissions/1908857387/).  Let n be the input length, and m be `max-min+1`&#x20;
    * TC: $$O(nlogm)$$
    * SC: $$O(m)$$
* :red\_circle: LC 354. Russian Doll Envelopes
  * It's not a DP question but I add it here because it relates to above LC 300.
  * Key points
    * It's actually a **2D version of LIS** (LC 300). We can **sort 1st dimension** and **do LIS on 2nd dimension**.
    * For sorting, you need a clever trick to solve some edge cases (when 1st dimensions of different elements are equal)
  * [Optimal Answer](https://leetcode.com/problems/russian-doll-envelopes/submissions/1511895845). TC: $$O(n*log{n})$$, SC: $$O(n)$$
* :star2: LC 674. Longest Continuous Increasing Subsequence
  * Similar to LC 300
  * [Optimal Answer](https://leetcode.com/problems/longest-continuous-increasing-subsequence/submissions/1761751462/). TC: $$O(n)$$, SC: $$O(1)$$
* :star2: :white\_circle: LC 718. Maximum Length of Repeated Subarray
  * `dp[i][j]`: max length of repeated subarray including `nums1[i-1]` and `nums2[j-1]`. Use `i-1` and `j-1` because it's easy to implement it without doing extra initialization.
  * It's easy to make mistakes when you want to compress it to a 1D dp array.
  * [Optimal Answer](https://leetcode.com/problems/maximum-length-of-repeated-subarray/submissions/1456864029/). TC: $$O(m*n)$$, SC: $$O(n)$$
* :star2: :white\_circle: LC 1143. Longest Common Subsequence
  *   `dp[i][j]`: max length of common subsequence between `nums1[0:i-1]` and `nums2[0:j-1]`. **It does NOT require that common sequence must include nums1\[i-1] and nums2\[j-1] like LC 718 and LC 674**

      > 求递增序列的时候，因为要求序列有序，所以必须确定序列最后一个元素的值，才能比较新加入序列的元素是不是递增的。求相等序列的时候，如果求连续相等子序列，则还是要确定序列最后一个元素的值；但是本题求的是不必连续的相等子序列，就不需要知道序列最后一个元素的值，只要知道范围内相等的序列长度就行，新来的相等元素可以直接加在序列后面
  * [Optimal Answer](https://leetcode.com/problems/longest-common-subsequence/submissions/1470569648). TC: $$O(M*N)$$, SC: $$O(min(M,N))$$
    * Compressing space needs a special technique.
* LC 1035. Uncrossed Lines
  * Same as above LC 1143
  * [Optimal Answer](https://leetcode.com/problems/uncrossed-lines/submissions/1761950446/).  TC: $$O(M*N)$$, SC: $$O(min(M,N))$$
* :orange\_circle: LC 3202. Find the Maximum Length of Valid Subsequence II
  * [Optimal Answer](https://leetcode.com/problems/find-the-maximum-length-of-valid-subsequence-ii/submissions/1909970543). TC: $$O(n*k)$$, SC: $$O(k^2)$$
* :orange\_circle: LC 898. Bitwise ORs of Subarrays
  * This problem isn’t about computing every subarray OR (which leads to $$O(n^2)$$), but about realizing that **for each ending index, the number of distinct OR results is bounded (\~32).**
  * I was enumerating all subarrays (all dp\[i]\[j]), but the real insight is that for each fixed right endpoint j, the number of **distinct OR states** is bounded (\~32), so the optimization comes from compressing the state space rather than scanning all i.
  * [Optimal Answer](https://leetcode.com/problems/bitwise-ors-of-subarrays/submissions/1927842953). where $$N$$ is the length of `A`, and $$W$$ is the maximum size of elements in `A` , TC: $$O(n*logW)$$, SC: $$O(n*logW)$$

#### :jigsaw: **Edit Distance series**

* Notes
  * The overall approach is very similar. All problems can be simplified into a 1D array, but it’s best to start with a 2D array because it’s easier to understand that way.
  * DP array using `dp[s.length()+1][t.length()+1]`: Initialization is more convenient and allows for unified logic handling.
  * Operations
    * Delete: LC 392, 115, 583
    * Delete/Insert/Update: LC 72
* LC 392. Is Subsequence
  * :white\_circle: Method 1: 2-pointers. Its performance is better DP and it's super easy to implement;&#x20;
    * [Optimal Answer](https://leetcode.com/problems/is-subsequence/submissions/1463718029). TC: $$O(n)$$, SC: $$O(1)$$
  * Method 2: DP. Need to realize it's very similar to LC 1143.
    * [Answer](https://leetcode.com/problems/is-subsequence/submissions/1762043049/). TC: $$O(m*n)$$, SC: $$O(min(m,n))$$
* :red\_circle: LC 115. Distinct Subsequences
  * Hint: Only do deletion on String s
  * [Optimal Answer](https://leetcode.com/problems/distinct-subsequences/submissions/1763037505/). TC: $$O(m*n)$$, SC: $$O(min(m,n))$$
* LC 583. Delete Operation for Two Strings
  * Method 1: Use DP to resolve it directly. [Optimal Answer](https://leetcode.com/problems/delete-operation-for-two-strings/submissions/1763109666/). TC: $$O(m*n)$$, SC: $$O(min(m,n))$$
  * Method 2: Use the DP solution of LC 1143 to resolve it
* :star2: LC 72. Edit Distance
  * [Optimal Answer](https://leetcode.com/problems/edit-distance/submissions/1470586491). TC: $$O(M*N)$$, SC: $$O(min(M,N))$$
* :orange\_circle: LC 97. Interleaving String
  * I came up with approach-1 after spending a lot of time, but that's not the best way (the way of defining the state transition function) to solve this problem.
  * Assume n1 = length of `s1`, n2 = length of `s2`.
  * Approach 1 (My solution)
    * TC: $$O((n1 + n2)*min(n1, n2))≤O(n1*n2)$$, SC: $$O(min(n1, n2))$$
  * :thumbsup: Approach 2 (LeetCode solution)
    * $$TC: O(n1*n2), SC: O(n2)$$

#### :jigsaw: **Palindromic String**

* Notes
  * Use `dp[i][j]` to iterate each substring (`s[i]` to `s[j]`) case.
* :white\_circle: LC 647. Palindromic Substrings
  * [Optimal Answer](https://leetcode.com/problems/palindromic-substrings/submissions/1460425743/). TC: $$O(n^2)$$, SC: $$O(n)$$
* :star2: LC 5. Longest Palindromic Substring
  * [Optimal Solution](https://leetcode.com/problems/longest-palindromic-substring/submissions/1477332644). TC: $$O(n^2)$$, SC: $$O(n)$$
* :star2: LC 516. Longest Palindromic Subsequence
  * [Optimal Answer](https://leetcode.com/problems/longest-palindromic-subsequence/submissions/1460431823/). TC: $$O(n^2)$$, SC: $$O(n)$$
* :orange\_circle: LC 3472. Longest Palindromic Subsequence After at Most K Operations
  * It's a combination of an advanced version of LC 516 + Knapsack ideas
  * [Optimal Answer](https://leetcode.com/problems/longest-palindromic-subsequence-after-at-most-k-operations/submissions/1567570744/). TC: $$O(n*n*k)$$, SC: $$O(n*n*k)$$

#### DP on Tree

* LC 2858. Minimum Edge Reversals So Every Node Is Reachable
  * [Optimal Answer](https://leetcode.com/problems/minimum-edge-reversals-so-every-node-is-reachable/submissions/1920425023). TC: $$O(n)$$, SC: $$O(n)$$
