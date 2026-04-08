---
description: Notes and typical questions for Math related questions
icon: calculator-simple
---

# Math

## **Notes**

* When the **order** of a list does **NOT** matter, how do you **remove an element in** $$O(1)$$? Override that element using the last element first and then remove the last element of the array.

## **Typical Questions**

### **General Math Questions**

* :white\_circle: LC 9. Palindrome Number
  * [Optimal Answer](https://leetcode.com/problems/palindrome-number/submissions/1475741807). TC: $$O(log_{10}{n})$$, SC: $$O(1)$$
* :white\_circle: LC 13. Roman to Integer
  * [Optimal Answer](https://leetcode.com/problems/roman-to-integer/submissions/1476579423).
    * TC: $$O(1)$$, this is because the input Roman number has an upper limit of 3999 which is a constant
    * SC: $$O(1)$$
* LC 12. Integer to Roman
  * I feel my answer is better than the LeetCode editorial because it has fewer hardcoded values.
  * [Optimal Answer](https://leetcode.com/problems/integer-to-roman/submissions/1769744873). TC: $$O(1)$$, SC: $$O(1)$$
* :orange\_circle: LC 7. Reverse Integer
  * `Integer.MAX_VALUE` = $$2^{31}-1 = 2147483647$$
  * `Integer.MIN_VALUE` = $$-2^{31} = -2147483648$$
  * [Optimal Answer](https://leetcode.com/problems/reverse-integer/submissions/1479954952). TC: $$O(n)$$, SC: $$O(1)$$
* :orange\_circle: LC 31. Next Permutation
  * This can also be categorized as 2 pointers or greedy.
  * Ideas
    * To make the permutation larger, we need to swap a `leftNum` with a `rightNum` and `leftNum < rightNum`
    * To make the smallest larger permutation
      * Find **rightmost** valid `leftNum`, keep checking the **pair of two successive numbers** from the end of the array. The sequence **starting from "leftNum index + 1"** to the end of the array must be in **descending** order.
      * Find the **rightmost** valid `rightNum`, and keep checking numbers from "leftNum index + 1" to the end of the array
      * After the swap, **Reverse** the sequence starting **from "leftNum index + 1"** to the end of the array because it's in **descending** order, and reversing it can make the final valid answer smaller.
  * [Optimal Answer](https://leetcode.com/problems/next-permutation/submissions/1480023556). TC: $$O(n)$$, SC: $$O(1)$$
* :orange\_circle: LC 50. Pow(x, n)
  * Its implementation is more complicated than I thought...
  * [Optimal Answer](https://leetcode.com/problems/powx-n/submissions/1484817375). TC: $$O(logn)$$, SC: $$O(1)$$
* :white\_circle: LC 202. Happy Number
  * It's easy to overlook the solution with constant space complexity.
  * Explanation: [https://leetcode.com/problems/happy-number/description/comments/1566928/](https://leetcode.com/problems/happy-number/description/comments/1566928/)
  * [Optimal Answer](https://leetcode.com/problems/happy-number/submissions/1505472460)
    * TC: $$O(logn)$$, it's very difficult to get this number. Check the analysis in the LC editorial.
      * > great explanation! For approach 1, I will add a little bit of my own explanation because it may help a little. For the time complexity, the way we reach O(log N) is as so: first we follow this link ([https://stackoverflow.com/a/50262470](https://stackoverflow.com/a/50262470)) to understand why summing the digits of a number is O(log N), where N is the number itself. So for our time complexity analysis, we will take this fact for granted (that the getNext() method is O(logN). The time complexity analysis is broken up into two steps:
        >
        > \[based off of the insight that once a number reaches the <=243 threshold, it cannot get above it again]
        >
        > 1. the amount of time it takes for a number to reach 243
        > 2. once a number reaches the <=243 threshold, the amount of type it takes to either a. discover a cycle or b. get to 1
        >
        > For step 1) we argue that the number of time to reach 243 is O(log N) + O(log log N) + ..., but we disregard the terms after O(log N) because they are insignificant compared with O(log N). So the time for step 1 is O(log N)
        >
        > For step 2) we argue that once a number reaches the <= 243 threshold, it will take at absolute worst case, 243 more getNext() calls before we a. reach cycle or b. get to 1. so each getNext call is O(log N) or O(d), where d is number of digits, this is the equivalent statement. so each getNext call here is O(3), or just 3. And we know that at absolute MOST we will have 243 more getNext calls, so 243 \* 3 is the time complexity here.
        >
        > Adding the two steps together we get O(log N) + O(243 \* 3), and in Big O constants drop out so we get O(log N) as our time complexity.
        >
        > Wrote this a bit quick, so excuse the grammar errors and poor structure lol. Hope this helps!
    * SC: $$O(1)$$
* :red\_circle: LC 843. Guess the Word
  * [Optimal Answer](https://leetcode.com/problems/guess-the-word/solutions/556075/how-to-explain-to-interviewer-843-guess-the-word). TC: $$O(n)$$, SC: $$O(n)$$
* :white\_circle: LC 380. Insert Delete GetRandom O(1)
  * Learned how to delete a specific item in `ArrayList` in TC $$O(1)$$.
  * [Optimal Answer](https://leetcode.com/problems/insert-delete-getrandom-o1/submissions/1512976417).
    * TC: For all functions, $$O(1)$$
      * SC: $$O(n)$$
* :orange\_circle: LC 2013. Detect Squares
  * [Optimal Answer](https://leetcode.com/problems/detect-squares/submissions/1544449276/).
    * Let $$N$$ be the number of points
    * `add(...)` : TC $$O(1)$$
    * `count(...)` : TC $$O(N)$$
    * SC: $$O(N)$$
* :white\_circle: LC 2364. Count Number of Bad Pairs
  * I used a very convoluted approach with TC $$O(n)$$ to solve this problem, but that's not ideal. The problem should be cleverly solved by using the given equation in the problem statement and making transformations.
  * [Optimal Answer](https://leetcode.com/problems/count-number-of-bad-pairs/submissions/1560725337). TC: $$O(n)$$, SC: $$O(n)$$
* :white\_circle: LC 2965. Find Missing and Repeated Values
  * [Optimal Answer](https://leetcode.com/problems/find-missing-and-repeated-values/submissions/1567444650). TC: $$O(n^2)$$, SC: $$O(n^2)$$
* :white\_circle: LC 66. Plus One
  * [Optimal Answer](https://leetcode.com/problems/plus-one/submissions/1496716023). TC: $$O(n)$$, SC: $$O(n)$$
* :orange\_circle: LC 172. Factorial Trailing Zeroes
  * [Optimal Answer](https://leetcode.com/problems/factorial-trailing-zeroes/submissions/1875808105). TC: $$O(logn)$$, SC: $$O(1)$$
* :white\_circle: LC 149. Max Points on a Line
  * [Optimal Answer](https://leetcode.com/problems/max-points-on-a-line/submissions/1875913261). TC: $$O(n^2)$$, SC: $$O(n)$$
* :orange\_circle: LC 273. Integer to English Words
  * **English Number Grouping Rule:** English uses a **base-1000 grouping system** when reading and writing large numbers. Digits are grouped every three places: **thousand (10³), million (10⁶), billion (10⁹), trillion (10¹²)**. This differs from Chinese, which groups numbers by **10,000 (万)**. For example, 10,000 is read as _ten thousand_ in English, and 100,000,000 (一亿) is _one hundred million_.
  * [Optimal Answer](https://leetcode.com/problems/integer-to-english-words/submissions/1904898924). TC: $$O(log_{10}n)$$, SC: $$O(1)$$

### Enumeration / Brute Force

* LC 2048. Next Greater Numerically Balanced Number
  * [Optimal Answer](https://leetcode.com/problems/next-greater-numerically-balanced-number/submissions/1963232095).&#x20;
    * Let $$C=1224444$$ be the largest possible numerically balanced number based on the given constraints.
    * TC: $$O(C−n)$$.
    * SC: $$O(1)$$.

### Geometry

* :orange\_circle: LC 939. Minimum Area Rectangle
  * [Optimal Answer](https://leetcode.com/problems/minimum-area-rectangle/submissions/1479672294). TC: $$O(n^2)$$, SC: $$O(n)$$
* :red\_circle: LC 963. Minimum Area Rectangle II
  * How do you know if 4 points can form a rectangle?
    * > Notice that a necessary and sufficient condition to form a rectangle with two opposite pairs of points is that the points must have the **same center and radius**.
  * [Optimal Answer.](https://leetcode.com/problems/minimum-area-rectangle-ii/submissions/1528115788/) TC: $$O(n^2*log{n})$$, SC: $$O(n^2)$$
* LC 3195. Find the Minimum Area to Cover All Ones I
  * [Optimal Answer](https://leetcode.com/problems/find-the-minimum-area-to-cover-all-ones-i/submissions/1895894255/). TC: $$O(m*n)$$, SC: $$O(1)$$
* :red\_circle: LC 3197. Find the Minimum Area to Cover All Ones II
  * Core ideas
    * Firstly, think about how many ways there are to split an entire matrix into 3 rectangles.
    * Secondly, for each way, think about what you need to do for each rectangle.
  * [Optimal Answer](https://leetcode.com/problems/find-the-minimum-area-to-cover-all-ones-ii/submissions/1895779776). TC: $$O(m^2*n^2)$$, SC: $$O(m*n)$$
* :orange\_circle: LC 3025. Find the Number of Ways to Place People I
  * [Optimal Answer](https://leetcode.com/problems/find-the-number-of-ways-to-place-people-i/submissions/1899348011). TC: $$O(n^2)$$, SC: $$O(logn)$$
* LC 3047. Find the Largest Area of Square Inside Two Rectangles
  * [Optimal Answer](https://leetcode.com/problems/find-the-largest-area-of-square-inside-two-rectangles/submissions/1972071492). TC: $$O(n^2)$$, SC: $$O(1)$$
