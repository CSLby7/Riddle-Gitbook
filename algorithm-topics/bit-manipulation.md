---
description: Notes and typical questions for bits related problems
icon: binary
---

# Bit Manipulation

## **Notes**

* Binary to Decimal Conversion
  * $$1101_2$$\
    $$=1*2^3 + 0*2^2 + 1*2^1 + 1*2^0$$\
    $$=8+0+2+1=11$$
* Java `int` is 32 bits.
* Get the last bit of an int number: `int bit = n&1`
* Bit operation precedence is kind of low. Protect it with `()`
* XOR (exclusive OR)
  * Rules
    * `0 ^ a = a`
    * `a ^ a = 0`
    * `a ^ b ^ c = a ^ c ^ b`
  *   Use cases

      * Swap 2 var without temp var

      ```java
        int x = 10, y = 20;
        x = x ^ y;  // x becomes 30 (binary XOR of 10 and 20)
        y = x ^ y;  // y becomes 10 (original value of x)
        x = x ^ y;  // x becomes 20 (original value of y)
      ```

      * Find a Single Number in an Array. There are some special requirements on the array.
* Two's complementary (二进制补码)
  * In Java (and most modern systems), **negative** numbers are stored in **two’s complement** format.
    * If `n` is an integer, `-n = ~n+1` . In this way, -n+n will have zero in all bits
  * Also, based on this, `n&(-n)` is a way to **keep the rightmost 1-bit and to set all the other bits to 0**.
* Rolling Bitmask:&#x20;
  * Use case: Processing a fixed-size binary window. Use the hash as a compact window ID for checking, counting, or deduplicating binary patterns.
  * Core idea: The last k bits can be stored directly as an integer.
  * Update: `hash = ((hash << 1) & mask) | newBit`
  * Meaning:
    * `shift left` -> make room for the new bit
    * `& mask` -> keep only the last k bits
    * `| newBit` -> append the new bit
    * Mask: `mask = (1 << k) - 1`&#x20;
  * Invariant: After each update, hash represents the latest k-bit window.

## **Typical Questions**

* :star2: LC 191. Number of 1 Bits
  * Approach 1: Use `mask&n` to check each bit in `for` loop.
    * [Answer](https://leetcode.com/problems/number-of-1-bits/submissions/1471469668). TC: $$O(1)$$, SC: $$O(1)$$
  * :thumbsup: :orange\_circle: Approach 2: Bit Manipulation. Subtracting `1` from `n` flips all the bits to the right of the least significant `1` bit (including the `1` itself). Then performing `n & (n - 1)` **clears that least significant 1**.
    * [Answer](https://leetcode.com/problems/number-of-1-bits/submissions/1471472046).
      * TC: $$O(log{n})$$, where $$log{n}$$ is the maximum number of bits in a number
      * SC: $$O(1)$$
* :orange\_circle: LC 38. Counting Bits
  * It can be resolved by DP
  * [Optimal Answer](https://leetcode.com/problems/counting-bits/submissions/1471532321).
    * TC: $$O(n)$$
    * SC: $$O(n)$$
* :orange\_circle: LC 136. Single Number
  * [Optimal Answer](https://leetcode.com/problems/single-number/submissions/1471543078). TC: $$O(n)$$, SC: $$O(1)$$
* :orange\_circle: LC 137. Single Number II
  * [Optimal Answer](https://leetcode.com/problems/single-number-ii/submissions/1875692636). TC: $$O(n)$$, SC: $$O(1)$$
  * Reference: [https://leetcode.com/problems/single-number-ii/solutions/43297/java-on-easy-to-understand-solution-easi-qoxr](https://leetcode.com/problems/single-number-ii/solutions/43297/java-on-easy-to-understand-solution-easi-qoxr)
* :white\_circle: LC 1318. Minimum Flips to Make a OR b Equal to c
  * [Optimal Answer](https://leetcode.com/problems/minimum-flips-to-make-a-or-b-equal-to-c/submissions/1471560745).
    * Let `n` be the maximum length in the binary representation of `a`, `b` or `c`
    * TC: $$O(n)$$
    * SC: $$O(1)$$
* :orange\_circle: LC 231. Power of Two
  * [Optimal Answer](https://leetcode.com/problems/power-of-two/submissions/1554523829). TC: $$O(1)$$, SC: $$O(1)$$
* :star2: :orange\_circle: LC 190. Reverse Bits
  * [Optimal Answer](https://leetcode.com/problems/reverse-bits/submissions/1874732580). TC: $$O(1)$$, SC: $$O(1)$$
* :orange\_circle: LC 201. Bitwise AND of Numbers Range
  * [Optimal Answer](https://leetcode.com/problems/bitwise-and-of-numbers-range/submissions/1875704761). TC: $$O(1)$$, SC: $$O(1)$$
* :red\_circle: LC 751. IP to CIDR
  * [Optimal Answer](https://leetcode.com/problems/ip-to-cidr/submissions/1894098305). Assume the output size is $$k$$, TC: $$O(k)$$, SC: $$O(1)$$
* :orange\_circle: LC 2571. Minimum Operations to Reduce an Integer to 0
  * [Optimal Answer](https://leetcode.com/problems/minimum-operations-to-reduce-an-integer-to-0/submissions/1901645947). TC: $$O(logn)$$, SC: $$O(1)$$
* :white\_circle: LC 2749. Minimum Operations to Make the Integer Zero
  * [Optimal Answer](https://leetcode.com/problems/minimum-operations-to-make-the-integer-zero/submissions/1936298177). TC: $$O(1)$$, SC: $$O(1)$$
* :white\_circle: LC 1461. Check If a String Contains All Binary Codes of Size K
  * [Optimal Answer](https://leetcode.com/problems/check-if-a-string-contains-all-binary-codes-of-size-k/submissions/1989055912). TC: $$O(n)$$, SC: $$O(2^k)$$
* :orange\_circle: LC 3314. Construct the Minimum Bitwise Array I
  * [Optimal Answer](https://leetcode.com/problems/construct-the-minimum-bitwise-array-i/submissions/2052755035/). TC: $$O(nlogm)$$, SC: $$O(1)$$
* LC 3315. Construct the Minimum Bitwise Array II
  * Same as above.
