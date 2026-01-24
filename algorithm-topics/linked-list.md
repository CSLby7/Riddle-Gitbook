---
description: Notes and typical questions for linked list related problems
icon: link
---

# Linked List

## **Notes**

* When deleting a node with a specific value
  * Consider adding a dummyHead to unify the deletion logic
  * Make sure every node is visited. When doing deletion, you may skip some nodes mistakenly
  * The return value should be a new head. Usually, the new head is gotten from a var that does not change instead of a var that keeps changing.
* When designing a linked list class with some actions,
  * Be careful about `addAtTail` implementation when `size==0`
  * Using a dummyHead can simplify most implementation
*   Find mid node of a linked list

    * Without dummy head

    ```java
        ListNode slow = head;
        ListNode fast = head;

        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }

        // If the length of the list is even, slow points to 1st node of 2nd half of the list here
        // If the length of the list is odd, slow points to the exact mid node of the list here
    ```

    * With dummy head

    ```java
       ListNode dummyHead = new ListNode(0);
       dummyHead.next = head;
       ListNode slow = dummyHead;
       ListNode fast = dummyHead;

       while (fast != null && fast.next != null) {
           slow = slow.next;
           fast = fast.next.next;
       }

       // If the length of the list is even, slow points to the last node of 1st half of the list here
       // If the length of the list is odd, slow points to the exact mid node of the list here
    ```

## **Typical Questions (18)**

### **Other Linked List questions (4)**

* LC 707. Design Linked List
  * [Optimal Answer](https://leetcode.com/problems/design-linked-list/submissions/1683340747/).
* LC 2130. Maximum Twin Sum of a Linked List
  * :orange\_circle: Method 1: Mutate the original linked list.
    * [Answer](https://leetcode.com/problems/maximum-twin-sum-of-a-linked-list/submissions/1466048691). TC: $$O(n)$$, SC: $$O(1)$$
  * Method 2: Not Mutate the original linked list.
    * [Answer](https://leetcode.com/problems/maximum-twin-sum-of-a-linked-list/submissions/1466043592). TC: $$O(n)$$, SC: $$O(n)$$
* :white\_circle: LC 2. Add Two Numbers
  * Try not to do post-processing after `while` loop.
  * [Optimal Answer](https://leetcode.com/problems/add-two-numbers/submissions/1473907948). TC: $$O(max(m,n))$$, SC: $$O(1)$$ if not consider result space.
* :white\_circle: LC 138. Copy List with Random Pointer
  * Try to do it in 1 pass.
  * [Answer](https://leetcode.com/problems/copy-list-with-random-pointer/submissions/1792482495). TC: $$O(n)$$, SC: $$O(n)$$
    * The optimal answer can only use constant space, but it will modify input data, and it will do it in multiple passes.
* :white\_circle: LC 160. Intersection of Two Linked Lists
  * [Optimal Answer](https://leetcode.com/problems/intersection-of-two-linked-lists/submissions/1720014780/). TC: $$O(n)$$, SC: $$O(1)$$

### **Linked List Circle (2)**

* LC 141. Linked List Cycle
  * [Optimal Answer](https://leetcode.com/problems/linked-list-cycle/submissions/1070238652). TC: $$O(n)$$, SC: $$O(1)$$
* :white\_circle: LC 142. Linked List Cycle II
  * ![](<../.gitbook/assets/LC-142.drawio (1).png>)
  * Variables
    * x = length between start and entry point
    * y = length between circle entry and slow meet fast
    * z = length between slow meet fast and circle entry
    * t = time when slow node meet fast node
  * $$2(x+y)=x+y+n(y+z) => x=(n-1)(y+z)+z$$ 。
    * 由此推出x=z这个逻辑其实很绕。我换一个假设：$$x-z=(n-1)(y+z)$$。$$t1$$ 时刻慢指针再走 $$z$$ 步到达链入口。如果从入口点再走 $$x-z$$ 步依旧会在入口点（$$x-z$$ 是环长的整数倍数）。
    * 因此，$$t$$ 时刻，新node从start出发，slow node从“slow meet fast point”出发。等到slow到达circle entry时，新node距离circle entry还有 $$x-z$$ 步。由于 $$x-z$$ 是环长的整数倍数，当新node走到circle entry那一刻必定与slow node相遇。因此，由此可反推出新node与slow node相遇点一定为circle entry。
  * [Optimal Answer](https://leetcode.com/problems/linked-list-cycle-ii/submissions/1687759944/). TC: $$O(n)$$, SC:&#x20;

### Linked List Manipulation (4)

* LC 24. Swap Nodes in Pairs
  * [Optimal Answer](https://leetcode.com/problems/swap-nodes-in-pairs/submissions/1493006058). TC: $$O(n)$$, SC: $$O(1)$$
* :white\_circle: LC 61. Rotate List
  * Try to only have 2 `for`/`while` loops.
  * [Optimal Answer](https://leetcode.com/problems/rotate-list/submissions/1797909366). TC: $$O(n)$$, SC: $$O(1)$$
* :white\_circle: LC 86. Partition List
  * [Optimal Answer](https://leetcode.com/problems/partition-list/submissions/1798704413). TC: $$O(n)$$, SC: $$O(1)$$
* :orange\_circle: LC 328. Odd Even Linked List
  * Its idea is tricky. Go through the linked list with lengths of 5 and 6 respectively to check the terminal condition of `while` loop.
  * [Optimal Answer](https://leetcode.com/problems/odd-even-linked-list/submissions/1465999243). TC: $$O(n)$$, SC: $$O(1)$$

### Reverse Linked List (4)

* :star2: LC 206. Reverse Linked List
  * Know **both iterative and recursive** solutions
  * [Iterative Answer](https://leetcode.com/problems/reverse-linked-list/submissions/1466003384). TC: $$O(n)$$, SC: $$O(1)$$
  * [Recursive Answer](https://leetcode.com/problems/reverse-linked-list/submissions/1466007815). TC: $$O(n)$$, SC: $$O(n)$$
* LC 92 Reverse Linked List II
  * [Optimal Solution](https://leetcode.com/problems/reverse-linked-list-ii/submissions/1497909907). TC: $$O(n)$$, SC: $$O(1)$$
* :white\_circle: LC 25. Reverse Nodes in k-Group
  * I came up with approach 1 by myself!
  * Approach 1 with undo operation
    * [Answer](https://leetcode.com/problems/reverse-nodes-in-k-group/submissions/1795999019). TC: $$O(n)$$, SC: $$O(1)$$
  * :thumbsup: Approach 2 without undo operation
    * [Answer](https://leetcode.com/problems/reverse-nodes-in-k-group/solutions/11440/non-recursive-java-solution-and-idea/?envType=study-plan-v2\&envId=top-interview-150). TC: $$O(n)$$, SC: $$O(1)$$
* LC 234. Palindrome Linked List
  * Must modify the input linked list in place if we want to resolve it in SC $$O(1)$$
  * [Optimal Answer](https://leetcode.com/problems/palindrome-linked-list/submissions/1537466943). TC: $$O(n)$$, SC: $$O(1)$$

### Remove List Node (4)

* LC 203. Remove Linked List Elements
  * Know **both iterative and recursive** solutions
* LC 19. Remove Nth Node From End of List
  * Use **fast and slow pointers** to reduce explored items !!!
  * [Optimal Answer](https://leetcode.com/problems/remove-nth-node-from-end-of-list/submissions/1796937220). TC: $$O(n)$$, SC: $$O(n)$$
* LC 82. Remove Duplicates from Sorted List II
  * [Optimal Answer](https://leetcode.com/problems/remove-duplicates-from-sorted-list-ii/submissions/1796945757). TC: $$O(n)$$, SC: $$O(1)$$
* LC 2095. Delete the Middle Node of a Linked List
  * Dummy head node + 2 pointers. The solution is very clever by solving the question in 1 iteration
  * [Optimal Answer](https://leetcode.com/problems/delete-the-middle-node-of-a-linked-list/submissions/1465973317). TC: $$O(n)$$, SC: $$O(1)$$
