---
description: >-
  A quick reference for common coding principles and checks in programming,
  aimed at preventing errors and optimizing solutions.
icon: list
---

# Checklist for Programming Practices

## Java

* Every line ends with **';'** if using Java
* Check if it's possible to have an overflow in the code
  * e.g.: `long sum = (long) nums[i] + nums[j] + nums[k] + nums[l]`
* When comparing 2 lists of `ArrayList<Integer>`, (list1:\[200], list2:\[200]), you will find statement `list1.get(0) == list2.get(0)` is false, this is due to the reason below. Use `list1.get(0) - list2.get(0) == 0` or `list1.get(0).equals(list2.get(0))` to compare instead.

> This is because when you compare boxed primitives with the == operator in Java, you're actually doing a reference comparison, as opposed to a value comparison. However, if your value is between -127 and 128 inclusive, this == comparison will work though because Java interns those values. So you should avoid comparing boxed primitives like that. Instead use a.equals(b) or Objects.equals(a,b) if you're worried about nulls. This is actually a very good test that shows some of Java's quirks. \*\* as long as you haven't newed up the Integers yourself because in that case the references will be different and the == comparison will fail too.

* In Java, `Arrays.sort()` is implemented using a variant of the Quick Sort algorithm with a space complexity of $$O(logn)$$.

#### General

* Should have correct **return value** for each function
* Should **call** all necessary functions
* Check if `while/for` loop will exit at the beginning directly
  * e.g.: ListNode slow, fast = head, check if slow == fast at the beginning of loop

