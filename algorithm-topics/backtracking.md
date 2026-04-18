---
description: Notes and typical questions for backtracking algorithm
icon: nesting-dolls
---

# Backtracking

## **Notes**

* General code template

```java
private void backtracking(parameters) {
    if (termination condition) {
        collect result;
        return;
    }

    for (choose items to be processed in the same level) {
        process items;
        backtracking(parameters);
        restore status;
    }
}
```

* Permutation problems and Combination problems are very similar, differences are
  * Combination use `startIndex` to dedup in branch direction. Permutation use `used[]`/`Set` to dedup in branch direction. Reason: \[1,2] and \[2,1] are the same results in combination but different results in permutation. Therefore, in each level, `for` loop starts from `startIndex` in Combination but from `0` (skip items in `used[]`) in permutation.

## Typical Questions

### Combination

#### Notes

* Pick `k` or any number of items from `n` items w/o special requirement. **The order of results does** _**NOT**_ **matter**
* Handle pruning logic
  * Does not satisfy the requirement: In the 1st step of each level or the `for` loop if the input is sorted
  * Set end condition for `for` loop based on `k` value if `k` is a constant
* Handle dedup logic if necessary
* Termination condition and `return;` is not required for some cases because `for` loop itself can cover the termination condition. But I think it's still good to have it to make logic clear.
* **Subset problem**
  * It is a variation of combination problems. The key difference is that the **subset problem needs to collect results in** _**every node**_ but the **collection problem only collects results in** the _**leaf node**_. Subset problem = classic collection problem under this assumption
    * No requirement for `k`
    * No other requirement for the result (e.g. sum=target...)
  * It has another way of implementation. Pick each item or not in each level without using `for` loop in each level.

#### :jigsaw: **Unique** input items & Pick each item **once** & **`k` is a constant**

* Notes
  * `startIndex`: In `for` loop of each level, Pass the  current `i+1` as `startIndex` for the next level so that each item can be picked only once.
  * Prune
    * Set end condition for `for` loop based on `k` value
    * If necessary, do `return;` at the 1st step of each level if it already does not satisfy the requirement
  * Time complexity: $$O(n^{k})$$ (This is just the number of all combinations). $$k$$ is the number of elements we need to collect. $$n$$ is the length of input `candidates`. Theoretically, it should be $$O(C(n, k))$$. We are taking the upper limit(i.e., Big O) for easier calculation.
* :star2: :white\_circle: LC 77. Combinations
  * Make sure to **prune** during backtracking
  * [Optimal Answer](https://leetcode.com/problems/combinations/submissions/1424811245). TC: $$O(k*C(n,k))$$, SC: $$O(k)$$
* :white\_circle: LC 216. Combination Sum III
  * Similar to the above one. Do pruning for 2 cases (selection & sum).
  * Do NOT introduce any useless argument! For example, we can minus the sum in each level instead of having both `sum` and `target` arguments. We can use `path.size()` to check the termination condition instead of using another `index` argument.
  * [Optimal Answer](https://leetcode.com/problems/combination-sum-iii/submissions/1425758306). TC: $$O(k*C(9,k))$$, SC: $$O(k)$$
* :white\_circle: LC 17. Letter Combinations of a Phone Number
  * Use `String[]` to replace `Map` to optimize space a bit.
  * [Optimal Answer](https://leetcode.com/problems/letter-combinations-of-a-phone-number/submissions/1425764478). $$n$$ is the number of digits. TC: $$O(4^{n}*n)$$, SC: $$O(n)$$

#### :jigsaw: **Unique** input items & Pick each item **multiple times** & **No requirement for `k`**

* Notes
  * `startIndex`: In `for` loop of each level, Pass the current `i` as `startIndex` for the next level so that each item can be picked up multiple times.
  * Prune
    * Without sorting: Do this logic in the first step of each level
    * With sorting (Better): Put this logic into `for` loop to skip all other items within the same level if it already does not satisfy the requirement.
* :star2: :orange\_circle: LC 39. Combination Sum
  * Approach 1: [Answer](https://leetcode.com/problems/combination-sum/submissions/1742733598/) from Laioffer.
  * Approach 2: [Answer](https://leetcode.com/problems/combination-sum/submissions/1742737791/).
    * The solution can be further optimized by performing a second pruning, but the input needs to be sorted first.
    * TC: $$O((t/m) * n^{t/m+1})$$. $$n$$ is the length of the `candidates`; $$t$$ is the target sum; $$m$$ is the min value in the `candidates`. At each step, we can select any number any number of times. The maximum depth of the recursion tree would be $$t/m$$. At each level, we have n choices at max. At the end of each combination, we need to copy `path` into `result`.
    * SC: $$O(t/m)$$ for additional memory in the recursive function call stack.

#### :jigsaw: **Duplicate** input items & Pick each item **once** & **No requirement for `k`**

* Notes
  * Dedup: Need to sort the input first & skip items if `i != startIndex && input[i] == input[i-1]` in for loop
  * `startIndex`: In `for` loop of each level, pass, the current `i+1` as `startIndex` for the next level, so that each item can be picked only once.
  * Prune: Since the input is sorted first, this logic can be put into `for` loop to skip all other items within the same level if it already does not satisfy the requirement.
  * Time complexity: $$C(n,n)+C(n,n-1)+...+C(n,1) = 2^n$$. This is just the number of all combinations.
* :star2: :orange\_circle: LC 40. Combination Sum II
  * [Optimal Answer](https://leetcode.com/problems/combination-sum-ii/submissions/1425805705/).
    * TC: $$O(n*2^{n})$$. For each combination, we also need to copy `path` into `result` which is $$O(n)$$
    * SC: $$O(n)$$
* :star2: LC 90. Subsets II
  * [Optimal Answer](https://leetcode.com/problems/subsets-ii/submissions/1745696744/). TC: $$O(n*2^{n})$$. SC: $$O(n)$$
* :white\_circle: LC 491. Non-decreasing Subsequences
  * A variant of the above "LC 90. Subsets II". The difference is
    * Only collect results in some nodes with size >= 2
    * Cannot sort array to do dedup because it requires subsequence. Create local `used` variable using `Set`/`int[]` in each level.
  * [Optimal Answer](https://leetcode.com/problems/non-decreasing-subsequences/submissions/1745713566/). TC: $$O(n*2^{n})$$. SC:  $$O(n)$$

#### :jigsaw: **Unique** input items & Pick each item **once** & **No requirement for `k`**

* :orange\_circle: LC 131. Palindrome Partitioning
  * It's a variation of combination problems. Choose the place to do the partition, fix the left part, and then go to the next level to process the right side recursively
  * Optimation
    * Calculate Palindrome `dp[][]` in advance, so we do not need to check if each substring is a Palindrome during backtracking
    * Use same `StringBuilder` in the same level to store the left part
  * [Optimal Answer](https://leetcode.com/problems/palindrome-partitioning/submissions/1743886272/).
    * TC: $$O(n*2^n)$$
      * $$2^n$$ combinations: $$C(n,1) + C(n,2) + ... + C(n,n) = 2^n$$. (Cut once possibilities + Cut twice possibilities +...)
      * Need to copy `path` into `result` for each Combination
    * SC: $$O(n^2)$$
* :red\_circle: LC 93. Restore IP Addresses
  * Similar to the above LC 131, it is a string partition problem. **Very easy to make mistakes** in implementation.
  * Optimization
    * Convert input `String` to `StringBuilder` to modify it directly.
  * [Optimal Answer](https://leetcode.com/problems/restore-ip-addresses/submissions/1426799908/).
    * TC: $$O(3^4) = O(1)$$. The IP address can contain a maximum of 4 numbers, and each number can be split in up to 3 possible ways. Therefore, the maximum depth of the search tree is 4, and each node can have up to 3 child nodes.
    * SC: $$O(1)$$
* :star2: LC 78. Subsets
  * Most classic subsets problem. See notes under Combination.
  * TC: $$O(n*2^{n})$$, SC: $$O(n)$$
    * [Approach 1 with `for` loop](https://leetcode.com/problems/subsets/submissions/1570851297)
    * [Approach 2 without `for` loop](https://leetcode.com/problems/subsets/submissions/1570848916)

### **Permutations**

* Notes
  * Pick `k` (if `k` < `n`, it's a partial permutation) or any number of items from `n` items w/o special requirement **Order of result** _**MATTERS**_
  * Dedup
    * Use `used[]` (`used.length == nums.length`) to dedup in tree branch direction for all permutation problems regardless of unique input or duplicate input. `used[]` is similar to the `startIndex` used in combination problems.
  * Collect results in leaf nodes.

#### :jigsaw: **Unique** input items & Pick each item **once** & **`k` is a constant**

* :star2: LC 46. Permutations
  * [Optimal Answer](https://leetcode.com/problems/permutations/submissions/1130210956), TC: $$O(n * n!)$$, SC: $$O(n)$$

#### :jigsaw: **Duplicate** input items & Pick each item **once** & **`k` is a constant**

* Notes
  * Dedup: **In addition to `used[]`** to dedup in branch direction, we also need to dedup in tree level direction. There are 2 ways.
    * Method1: Sort the array first, then skip the item if `i!=0 && nums[i] == nums[i-1] && used[i-1] == false` in `for` loop
    * Method2: Create `used2[]` (`used2.length == value range of nums`) or `Set` in each level, then skip the item if `used2[nums[i]]` or `set.contains(nums[i])` in for loop.
* :star2: :white\_circle: LC 47. Permutations II
  * :thumbsup: Approach 1 with sort: [Answer](https://leetcode.com/problems/permutations-ii/submissions/1745861267/).
  * Approach 2 with `Set` : [Answer](https://leetcode.com/problems/permutations-ii/submissions/1745859359/).
  * TC: $$O(n * n!)$$, SC: $$O(n)$$

### **2D Backtracking**

* :star2: :orange\_circle: LC 51. N-Queens
  * Time Complexity: $$O(n^2 * n * n!)$$, $$n^2$$ for storing the result. $$n$$ for checking validation. $$n!$$ for all valid placements.
  *   Better solution to speed up validation,

      * Approach 1: use 3 extra `boolean[]`, 1st for column direction. Other 2 for diagonal direction. For how to know the diagonal index in those 2 `boolean[]` for a given point

      > In an nxn grid there are 2n - 1 diagonals going from top left corner to bottom right corner and there are 2n-1 diagonals going from top right corner to bottom left corner. The queen can run along both of these diagonal directions so we store both of them in boolean\[]s. We need to map every index to both of these diagonal boolean arrays to that indexes on the same diagonal map to the same index in the boolean array as seen below: Diagonals this way / \[ 0, 1, 2] \[ 1, 2, 3] \[ 2, 3, 4] need to map to boolean\[0,1,3,4] of size &#x32;_&#x6E; - 1 with the relation row + col. Diagonals this way \ \[ 2, 1, 0] \[ 3, 2, 1] \[ 4, 3, 2] need to map to boolean\[0,1,2,3,4] of size &#x32;_&#x6E; - 1 with the relation row + n - col - 1.

      * Approach 2: use 3 extra `Set`, 1st for column direction. Other 2 for diagonal direction. For each position `(r,c)`
        * column set: each position is encoded to `c`
        * diagonals set in this way \ : each position is encoded to `r-c`
        * diagonals set in this way / : each position is encoded to `r+c`
  * [Answer](https://leetcode.com/problems/n-queens/submissions/1495608614). TC: $$O(n!)$$, SC: $$O(n^2)$$
    * This is not the optimal solution with validation speedup but it's more understandable.
* :white\_circle: LC 52. N-Queens II
  * Trick: Use 3 sets to speed up position checking logic.
  * [Optimal Answer](https://leetcode.com/problems/n-queens-ii/submissions/1868837245). TC: $$O(n!)$$, SC: $$O(n)$$
* :orange\_circle: LC 37. Sudoku Solver
  * I come up with a solution which is different from 代码随想录. The main difference is that each level directly checks the position that needs to be visited as the next one instead of doing a traversal from `board[0][0]`.
  * Time complexity: $$9^{81}$$ in the worst case
* :white\_circle: LC 489. Robot Room Cleaner
  * [Optimal Answer](https://leetcode.com/problems/robot-room-cleaner/submissions/1982103569). TC: $$O(n)$$, SC: $$O(n)$$

### **Structured Generation with Constraints**

* LC 22. Generate Parentheses
  * [Optimal Answer](https://leetcode.com/problems/generate-parentheses/submissions/1492808398)
    * TC: $$O(n*2^{2n})$$. The accurate one is actually $$O(4^n/\sqrt{n})$$, this number is related to the Catalan number. It should be out of scope for interview.
    * SC: $$O(n)$$
* :orange\_circle: LC 3481. Apply Substitutions
  * [Optimal Answer](https://leetcode.com/problems/apply-substitutions/submissions/1589609871)
    * Let $$n$$ be the size of `replacements` , $$m$$ be the average length of `replacements` value's
    * TC: $$O(n+n^2*m+n*m)$$ ⇒ $$O(n^2*m)$$
    * SC: $$O(n)$$

### **Other Backtracking Problems**

* :red\_circle: LC 332. Reconstruct Itinerary
  * Method 1: Sort `<List<List<String>> tickets` by arrivals, then we can use the classic way to solve it with `used[]`. But this way will cause the **Time Limit Exceeded**
  * **Method 2**: Convert `<List<List<String>> tickets` to `Map<String, Map<String, Integer>>`. The nested `Map` should be `TreeMap` and it contains arrival and its count.
    * This is also TLE now. F\*\*k :smile:
    * > For those who get TLE on 80/81, don't by disheartened because some sick guy who has no life wants to show that he can screw up backtracking by creating a very dense graph, it is not your problem to not coming up with a pruning trick for certain use cases.
      >
      > It also a joke to expect someone come's up with an Eularian path finding algo without knowing it (which is the efficient algo for this type of problem). BTW, also don't read some of the "smart" solutions here that just copy the above algorithm and claims it is "just dfs" (although the code might look deceptively simple), these people have no idea why it works just pretend they have.
* :red\_circle: LC 679. 24 Game
  * [Optimal Answer](https://leetcode.com/problems/24-game/submissions/1906211998/). TC: $$O(n^3*n!*(n-1)!*3^{n-1})$$, SC: $$O(n^2)$$
* :red\_circle: LC 465. Optimal Account Balancing
  * > Key Insight
    >
    >
    >
    > Let n be the number of people with non-zero balances.&#x20;
    >
    >
    >
    > The optimal number of transactions is at most n−1, but this is not a tight bound for all cases. To understand it, think about selecting one person as a pivot and settling all others against it. Since the total balance is zero, the pivot will be automatically settled at the end. Therefore, the optimal number of transactions is always ≤ n−1.
    >
    >
    >
    > The minimum number of transactions is not always n−1; that is only a lower bound. The problem can be reframed as _**partitioning these balances into disjoint groups such that each group sums to zero**_. For a group of size k, at least k−1 transactions are required. Therefore, the total number of transactions equals:
    >
    > &#x20;                                               ∑(k−1) ⇒ n−g
    >
    > where g is the number of zero-sum groups.
    >
    > Thus, the problem reduces to **maximizing the number of zero-sum groups**.
    >
    > The DFS solution effectively enumerates all possible ways to merge balances (i.e., all possible groupings), and selects the one that produces the maximum number of zero-sum groups, which guarantees the minimum number of transactions.
  * [Answer](https://leetcode.com/problems/optimal-account-balancing/submissions/1950704428). TC: $$O((n-1)!)$$, SC: $$O(n)$$
