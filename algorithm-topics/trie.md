---
description: Notes and typical questions for Trie related problems
icon: spell-check
---

# Trie

## **Notes**

* Check the solution of LC 208 to see the template of `TrieNode`
  * Notice that either `boolean isEnd` or `String word` is feasible to mark a word in `TrieNode`

## **Typical Questions**

* :star2: :orange\_circle: LC 208. Implement Trie (Prefix Tree)
  * [Optimal Answer](https://leetcode.com/problems/implement-trie-prefix-tree/submissions/1472966746).
    * Let `m` be the length of the word
    * TC
      * `insert`: $$O(m)$$
      * `search`: $$O(m)$$
      * `prefix`: $$O(m)$$
    * SC
      * `insert`: $$O(m)$$
      * `search`: $$O(1)$$
      * `prefix`: $$O(1)$$
* :red\_circle: LC 1268. Search Suggestions System
  * Code is long and it's very easy to make mistakes during the implementation
  * [Optimal Answer](https://leetcode.com/problems/search-suggestions-system/submissions/1472990366/)
    * Let `N` be number of products, let `M` be the max length of the product, let `L` be the length of `searchWord`
    * TC: $$O(N*M+L(L+326*(M+M))$$
      * $$N*M$$ -> Tree Construction
      * $$L*(...)$$ -> for loop of each prefix of `searchWord`
      * $$...(L+...)$$ -> Find the last node of the given prefix
      * $$...(M+M)$$ -> Find each word takes <= $$M$$, call `toString()` of `StringBuilder` takes <= $$M$$
    * SC: $$O(N*M)$$
* :orange\_circle: LC 139. Word Break
  * Maybe thinking it in a normal DP way instead of a knapsack is more clear. Be careful about the boundary.
  * This question is also put in the DP section.
  * Given $$n$$ as the length of `s`, $$m$$ as the length of `wordDict`, and $$k$$ as the average length of the words in `wordDict`
    * [Straightforward DP Answer](https://leetcode.com/problems/word-break/submissions/1448983585).&#x20;
      * TC: $$O(n^3 + m*k)$$
      * SC: $$O(n+m*k)$$
    * [Optimal Answer](https://leetcode.com/problems/word-break/submissions/1505502045) (DP+Trie).
      * The idea of doing dp is different from the above straightforward one.
      * TC: $$O(n^2+m*k)$$
      * SC: $$O(n+m*k)$$
* LC 211. Design Add and Search Words Data Structure
  * Let `m` be the length of the word
  * TC
    * `addWord`: $$O(m)$$
    * `search`: $$O(26^m*m)$$
  * SC
    * `addWord`: $$O(m)$$
    * `search`: $$O(m)$$
* :orange\_circle: LC 212. Word Search II
  * 2 tricks for implementation.
    * **Remove words from the Trie during backtracking**\
      I initially used a separate function to remove matched words from the Trie to speed up execution. However, this cleanup step can be **merged directly into the DFS backtracking process**, which avoids extra traversals and makes the code both **more efficient and more elegant**.
    * **Store complete words in Trie nodes**\
      Instead of using a `StringBuilder` during DFS to construct the current path, a better approach is to **store the full word directly in the corresponding Trie node** (replacing the `isEnd` boolean flag).\
      When a word is found, it can be added to the result list immediately, eliminating string reconstruction and simplifying the DFS logic.
  * [Optimal Answer](https://leetcode.com/problems/word-search-ii/submissions/1867997612).&#x20;
    * Assume $$M$$ is the number of rows, $$N$$ is the number of columns, $$W$$ is the number of words, $$Lmax$$ is the max word length of those words,
    * TC: $$O(M*N*(4*3^{Lmax-1}))$$ &#x20;
    * SC: $$O(W*Lmax)$$
* :orange\_circle: LC 3043. Find the Length of the Longest Common Prefix
  * Damn, I should at least realize the HashMap solution. I feel so bad!
  * Approach 1 using HashMap. [Answer](https://leetcode.com/problems/find-the-length-of-the-longest-common-prefix/submissions/1915485629). TC: $$O(m*logm+n*logn)$$, SC: $$O(m*logm)$$
