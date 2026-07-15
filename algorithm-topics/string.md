---
description: Notes and typical questions for String related problems
icon: arrow-up-a-z
---

# String

## **Notes**

* In Java, When joining String, `new StringBuilder(s1).append(s2).toString()` is faster than `s1 + s2`

## **Typical Questions**

### **String Manipulation**

* :star2: LC 344. Reverse String
* LC 541. Reverse String II
* :star2: :white\_circle: LC 151. Reverse Words in a String
  * The most important part is how to **efficiently** remove leading/trailing spaces and duplicate spaces between words. Make that logic simple enough!
  * [Optimal Answer](https://leetcode.com/problems/reverse-words-in-a-string/submissions/1462946714/)
* Other platforms: Right shift of a string
  * It's not difficult, once you find the approach
* LC 1768. Merge Strings Alternately
* LC 345. Reverse Vowels of a String
* LC 443. String Compression
  * [Optimal Answer](https://leetcode.com/problems/string-compression/submissions/1463709973). TC: $$O(n)$$, SC: $$O(1)$$
* LC 67. Add Binary
  * [Optimal Answer](https://leetcode.com/problems/add-binary/submissions/1496726960). TC: $$O(n)$$, SC: $$O(n)$$
* :red\_circle: LC 761. Special Binary String
  * Super hard to understand question...
  * [Optimal Answer](https://leetcode.com/problems/special-binary-string/submissions/1882481834). TC: $$O(n^2)$$, SC: $$O(n)$$

### **KMP**

* Notes: the most important part is calculating `next[]`
* :star2: :orange\_circle: LC 28. Find the Index of the First Occurrence in a String
  * Assume the length of `haystack` is n and the length of `needle` is `m`
  * [Optimal Answer](https://leetcode.com/problems/find-the-index-of-the-first-occurrence-in-a-string/submissions/1856697640). TC: $$O(m+n)$$, SC: $$O(m)$$
* LC 459. Repeated Substring Pattern
  * A tricky way using `next[]` of KMP + Mathematical induction

### **String property**

* :red\_circle: LC 1071. Greatest Common Divisor of Strings
  * Check answer [https://leetcode.com/problems/greatest-common-divisor-of-strings/solutions/4470356/easy-clear-and-no-ambiguity-proof-based-on-editorial-ver/](https://leetcode.com/problems/greatest-common-divisor-of-strings/solutions/4470356/easy-clear-and-no-ambiguity-proof-based-on-editorial-ver/)
    * if `str1 + str2 != str2 + str1`, there must be no gcd string. It's easy to prove.
    * if `str1 + str2 == str2 + str1`, the divisible string must exist,
      * if the divisible string exists, it must be a prefix of either `str1` or `str2`
      * if the divisible string exists, the gcd string length must be the gcd of `str1` length and `str2` length
* LC 14. Longest Common Prefix
  * [Optimal Solution](https://leetcode.com/problems/longest-common-prefix/submissions/1477360462).
  * Let $$n$$ be the number of strings, $$m$$ be the minimum length of all strings
    * TC: $$O(n*m)$$
    * SC: $$(1)$$
  * :orange\_circle: Follow-up: Given a set of keys S = $$[S1​,S2​…Sn​]$$, find the longest common prefix among a string `q` and S. This LCP query will be called frequently.
    * Build a Trie based on all S and then find the common longest prefix.
* :red\_circle: LC 2663. Lexicographically Smallest Beautiful String
  * [Understandable Answer](https://leetcode.com/problems/lexicographically-smallest-beautiful-string/submissions/1478217162). TC: $$O(n^2*k)$$, SC: $$O(n)$$
  * Reference: [https://leetcode.com/problems/lexicographically-smallest-beautiful-string/solutions/3468265](https://leetcode.com/problems/lexicographically-smallest-beautiful-string/solutions/3468265)
* :white\_circle: LC 125. Valid Palindrome
  * Ease of making mistakes during implementation
  * [Optimal Answer](https://leetcode.com/problems/valid-palindrome/submissions/1498949343). TC: $$O(n)$$, SC: $$O(1)$$
* LC 3110. Score of a String
  * [Optimal Answer](https://leetcode.com/problems/score-of-a-string/submissions/1510914439).  TC: $$O(n)$$, SC: $$O(1)$$
* :white\_circle: LC 1422. Maximum Score After Splitting a String
  * The one-pass solution is really beautiful! I didn't realize this problem could be resolved using a one-pass solution when I wrote my own answer with the same TC.
  * [Optimal Answer](https://leetcode.com/problems/maximum-score-after-splitting-a-string/submissions/1542275526). TC: $$O(n)$$, SC: $$O(1)$$
* :red\_circle: LC 336. Palindrome Pairs
  * Read that good editorial carefully...
  * [Optimal Answer](https://leetcode.com/problems/palindrome-pairs/submissions/1597822437).
    * Let $$n$$ be the number of words and $$k$$ be the max length of single word
    * TC: $$O(k^2*n)$$
    * SC: $$O(k*n+k^2+n^2)$$

### **String Traversal**

* :white\_circle: LC 6. Zigzag Conversion
  * [Optimal Solution](https://leetcode.com/problems/zigzag-conversion/submissions/1483309431). TC: $$O(n)$$, SC: $$O(1)$$
* :white\_circle: LC 8. String to Integer (atoi)
  * [Optimal Solution](https://leetcode.com/problems/string-to-integer-atoi/submissions/1492186623). TC: $$O(n)$$, SC: $$O(1)$$
* :white\_circle: LC 58. Length of Last Word
  * [Optimal Answer](https://leetcode.com/problems/length-of-last-word/submissions/1770042735). TC: $$O(n)$$, SC: $$O(1)$$
* :white\_circle: LC 3136. Valid Word
  * [Optimal Answer](https://leetcode.com/problems/valid-word/submissions/1907426573). TC: $$O(n)$$, SC: $$O(1)$$

### Simulation

* :white\_circle: LC 68. Text Justification
  * [Optimal Answer](https://leetcode.com/problems/text-justification/submissions/1772262947).&#x20;
    * Let $$n$$ be `words.length`, $$k$$ be the average length of a word, and $$m$$ be `maxWidth`
    * TC: $$O(n*k)$$
    * SC: $$O(m)$$
* LC 412. Fizz Buzz
  * [Optimal Answer](https://leetcode.com/problems/fizz-buzz/submissions/1942464593). TC: $$O(n)$$, SC: $$O(1)$$
