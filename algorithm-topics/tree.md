---
description: Notes and typical questions for Tree related problems
icon: tree-christmas
---

# Tree

## ,**Notes**

* BFS vs DFS
  * DFS
    * Path-related problems because it can examine each path before moving on to the next.
  * BFS
    * Level-related problem.
* As we know, the maximal number of nodes in N-ary tree of $$H$$ height would be $$N^{H+1}$$
  * $$1+N+N^2+....+N^H$$ (等比数列)

## **Typical Questions (53)**

### **Preorder/Inorder/Postorder Traversal (4)**

* LC 144. Binary Tree Preorder Traversal
  * Order: Middle, Left, Right
  * **Recursive way**: Basic
  * :orange\_circle: **Iterative way**: It is straightforward to use a stack
    * [Optimal Answer](https://leetcode.com/problems/binary-tree-preorder-traversal/submissions/1723764740/). TC: $$O(n)$$, SC: $$O(h)$$ -> I think SC is O(h) instead of O(n) listed in leetcode solution.
* LC 145. Binary Tree Postorder Traversal
  * Order: Left, Right, Middle
  * **Recursive way**: Basic
  * **Iterative way**
    * Method 1: Depend on preorder traversal (Need to modify a little bit: swap left and right, then swap the entire result at the end)
      * [Optimal Answer](https://leetcode.com/problems/binary-tree-postorder-traversal/submissions/1096808282/). TC: $$O(n)$$, SC: $$O(h)$$
    * :orange\_circle: Method 2: Do postorder traversal from scratch. Need one variable to store the previously polled `TreeNode` so that we can know if the current should be polled during this visit.
      * [Optimal Answer](https://leetcode.com/problems/binary-tree-postorder-traversal/submissions/1723828966/). TC: $$O(n)$$, SC: $$O(n)$$
* LC 94. Binary Tree Inorder Traversal
  * Order: Left, Middle, Right
  * **Recursive way**: Basic
  * :red\_circle: **Iterative way**: **VERY HARD** to recall the correct solution. In addition to the stack itself, we need another variable (TreeNode pointer) to traverse the tree in inorder. This variable can notify us whether we should poll a node in the stack (collect the result) or continue exploring to the left.
    * [Optimal Answer](https://leetcode.com/problems/binary-tree-inorder-traversal/submissions/1096856841/). TC: $$O(n)$$, SC: $$O(n)$$
* LC 173. Binary Search Tree Iterator
  * [Optimal Answer](https://leetcode.com/problems/binary-search-tree-iterator/submissions/1804675805). TC for each call in average: $$O(1)$$, SC: $$O(h)$$

### :jigsaw: **Level Order Traversal (12)**

* Notes
  * Space complexity
    * Let w be the maximum number of nodes at any level (the tree’s **width**). The queue size is $$O(w)$$.
      * For a binary tree, $$w≤n$$ and in the worst case, $$w≤⌈n/2⌉$$ (when the last level is \~$$n/2$$ nodes, e.g., a complete/perfect tree).
* LC 102. Binary Tree Level Order Traversal
  * [Optimal Answer](https://leetcode.com/problems/binary-tree-level-order-traversal/submissions/1725070304/). TC: $$O(n)$$, SC: $$O(n)$$
    * > Space complexity = O( max number of nodes on a level), for a full and complete binary tree(worst case) last level which has all the leaf nodes will have the max number of nodes.\
      > Number of leaf nodes is given by (n+1)/2, so ignoring the constants makes the space complexity O(N)
* LC 107. Binary Tree Level Order Traversal II
* LC 199. Binary Tree Right Side View
  * [Optimal Answer](https://leetcode.com/problems/binary-tree-right-side-view/submissions/1405486463). TC: $$O(n)$$, SC: $$O(w+height)$$, where $$w$$ is the number of nodes in the widest level of the binary tree.
* LC 637. Average of Levels in Binary Tree
* LC 429. N-ary Tree Level Order Traversal
* LC 515. Find Largest Value in Each Tree Row
* LC 116. Populating Next Right Pointers in Each Node
  * Need to change the visit order for each level
* LC 117. Populating Next Right Pointers in Each Node II
  * Approach 1 with classic BFS queue: [Answer](https://leetcode.com/problems/populating-next-right-pointers-in-each-node-ii/submissions/1861933927). TC: $$O(n)$$, SC: $$O(n)$$
    * Need to change the visit order for each level
  * :thumbsup: :orange\_circle: Approach 2: [Optimal Answer](https://leetcode.com/problems/populating-next-right-pointers-in-each-node-ii/submissions/1861937808). TC: $$O(n)$$, SC: $$O(1)$$
* LC 104. Maximum Depth of Binary Tree
  * Method 1: Recursive way
    * [Optimal Answer](https://leetcode.com/problems/maximum-depth-of-binary-tree/submissions/1466061817). TC: $$O(n)$$, SC: $$O(Height)$$
  * Method 2: Iterative way (level order traversal)
* LC 111. Minimum Depth of Binary Tree
  * Be careful about the definition of Minimum Depth
  * Method 1: Recursive way
  * Method 2: Iterative way (level order traversal)
* LC 559. Maximum Depth of N-ary Tree
  * Method 1: Recursive way
  * Method 2: Iterative way (level order traversal)
* LC 1161. Maximum Level Sum of a Binary Tree
  * [Optimal Answer](https://leetcode.com/problems/maximum-level-sum-of-a-binary-tree/submissions/1466845369). TC: $$O(n)$$, SC: $$O(w)$$, where $$w$$ is the number of nodes in the widest level of the binary tree.
* :white\_circle: LC 103. Binary Tree Zigzag Level Order Traversal
  * Use `LinkedList` to avoid complicated logic.
  * [Optimal Answer](https://leetcode.com/problems/binary-tree-zigzag-level-order-traversal/submissions/1805217876). TC: $$O(n)$$, SC: $$O(n)$$
* LC 339. Nested List Weight Sum
  * [Optimal Answer](https://leetcode.com/problems/nested-list-weight-sum/submissions/1885442851). TC: $$O(n)$$, SC: $$O(n)$$
* LC 314. Binary Tree Vertical Order Traversal
  * [Optimal Answer](https://leetcode.com/problems/binary-tree-vertical-order-traversal/submissions/1887403024). TC: $$O(n)$$, SC: $$O(n)$$
* :orange\_circle: LC 364. Nested List Weight Sum II
  * When you encounter a mathematical formula, don’t rush to compute it directly. First, try to understand whether it can be interpreted from a different perspective. Reframing the formula may allow you to design a process that naturally produces the result, which is often simpler and more efficient than direct computation.
  * [Optimal Answer](https://leetcode.com/problems/nested-list-weight-sum-ii/submissions/1980626829). TC: $$O(n)$$, SC: $$O(n)$$

### **Tree Manipulation (3)**

* :star2: :white\_circle: LC 226. Invert Binary Tree
  * Make the solution accepted in the submission!!!
  * [Optimal Answer](https://leetcode.com/problems/invert-binary-tree/submissions/1861871662). TC: $$O(n)$$, SC: $$O(h)$$
* :white\_circle: LC 1110. Delete Nodes And Return Forest
  * [Optimal Answer](https://leetcode.com/problems/delete-nodes-and-return-forest/submissions/1509906550). TC: $$O(n)$$, SC: $$O(n)$$
* LC 114. Flatten Binary Tree to Linked List
  * :white\_circle: Approach 1: [Recursive solution](https://leetcode.com/problems/flatten-binary-tree-to-linked-list/submissions/1799788602). TC: $$O(N)$$, SC: $$O(N)$$. Post-order traversal can have shorter code than pre-order traversal.
  * Approach 2: [Iterative solution](https://leetcode.com/problems/flatten-binary-tree-to-linked-list/submissions/1799790596) using a stack. TC: $$O(N)$$, SC: $$O(N)$$.
  * :thumbsup: :orange\_circle: Approach 3: [Optimal iterative solution](https://leetcode.com/problems/flatten-binary-tree-to-linked-list/submissions/1799798134) with the same ideology as **Morris Traversal.**&#x20;
    * TC: $$O(N)$$. Each node will be processed at most twice.
    * SC: $$O(1)$$

### **Tree Comparison (4)**

* LC 101. Symmetric Tree
  * Just need to do traversal for 2 trees at the same time.
* LC 100. Same Tree
  * Similar to the above one
* :red\_circle: LC 572. Subtree of Another Tree
  * Depends on "_LC 100. Same Tree"_ in a helper function way
  * Be careful about null check
  * Be careful about which function gets called during recursion.
* LC 617. Merge Two Binary Trees

### **Tree Property (6)**

* LC 222. Count Complete Tree Nodes
  * [Optimal Answer](https://leetcode.com/problems/count-complete-tree-nodes/submissions/1407707251/). The best solution is $$O(logn * logn)$$
    * Check how to calculate this time complexity in the LC submission notes
    * Another way to understand it: $$T(n)=T(n/2)+O(logn)$$ => $$logn * logn$$ (ask GPT why)
* :orange\_circle: LC 110. Balanced Binary Tree
  * Be sure to skillfully utilize the return value of the recursive function to get the final result in **ONE** traversal
  * Be sure to return the result in advance to speed up the calculation
* :star2: LC 236. Lowest Common Ancestor of a Binary Tree
  * Assumptions: `p != q`, `p` and `q` will exist in the tree, All `Node.val` are unique.
  * 2 cases:
    1. `p` and `q` has LCA which is another node `s`.
    2. One of `p` and `q` is LCA for another node.
  * [Optimal Answer](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/submissions/1466744048). TC: $$O(n)$$, SC: $$O(height)$$
* :white\_circle: LC 1650. Lowest Common Ancestor of a Binary Tree III
  * I can’t believe I didn’t realize this problem is the same as LC 160 !!!
  * Approach 1 using Set: [Answer](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree-iii/submissions/1886406454). TC: $$O(height)$$, SC: $$O(height)$$
  * :thumbsup: Approach 2 without Set: [Optimal Answer](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree-iii/submissions/1886399768). TC: $$O(height)$$, SC: $$O(1)$$
* LC 1257. Smallest Common Region
  * Use `HashMap` and `HashSet` to simulate the LCA process.
  * [Optimal Answer](https://leetcode.com/problems/smallest-common-region/submissions/1605996988).&#x20;
    * Let $$m$$ be the number of region arrays, and let $$n$$ be the number of regions in each array.
      * TC: $$O(m*n)$$
      * SC: $$O(m*n)$$
* :red\_circle: LC 2458. Height of Binary Tree After Subtree Removal Queries
  * Idea: Try to think in the way of checking the height of each node by preorder traversal
  * [Optimal Answer](https://leetcode.com/problems/height-of-binary-tree-after-subtree-removal-queries/submissions/1511811481). TC: $$O(n+q)$$, SC: $$O(n)$$

### **Tree Path (10)**

* :white\_circle: LC 257. Binary Tree Paths
  * Be careful about how to store results during traversal
  * This is kind of a **backtracking** problem. Remember to **reset the status** in each recursion level
  * Optimal Answer. TC: $$O(n*log{n})$$, SC: $$O(n)$$
* :white\_circle: LC 112. Path Sum
  * Be careful about corner case: empty tree
  * [Optimal Answer](https://leetcode.com/problems/path-sum/submissions/1800977308). TC: $$O(n)$$, SC: $$O(n)$$
* :white\_circle: LC 113. Path Sum II
  * Not difficult but easy to make mistakes when storing results.
* :star2: :orange\_circle: LC 437. Path Sum III
  * It's kind of hard to figure out the solution using DFS + HashMap
  * [Optimal Answer](https://leetcode.com/problems/path-sum-iii/submissions/1466131089). TC: $$O(n)$$, SC: $$O(height)$$
* LC 513. Find Bottom Left Tree Value
  * Method 1: Iterative way. Easy to implement and understand.
  * :white\_circle: Method 2: Recursive way. Do it in **ONE** traversal. Remember that all traversal methods (Pre/In/Post order) **always visit the left node first** by default. This can simplify recursion logic at each level.
* LC 404. Sum of Left Leaves
  * The solution without a helper function is kind of hard to understand. Having a helper function with a flag may be a better way.
* :white\_circle: LC 1448. Count Good Nodes in Binary Tree
  * Do not use extra space!
  * [Optimal Answer](https://leetcode.com/problems/count-good-nodes-in-binary-tree/submissions/1466103419). TC: $$O(n)$$, SC: $$O(height)$$
* :white\_circle: LC 1372. Longest ZigZag Path in a Binary Tree
  * [Optimal Answer](https://leetcode.com/problems/longest-zigzag-path-in-a-binary-tree/submissions/1466733251). TC: $$O(n)$$, SC: $$O(height)$$
* :red\_circle: 124. Binary Tree Maximum Path Sum
  * I made it by myself! The editorial solution is more elegant in implementation. (I failed to make it the second time....)
  * [Optimal Answer](https://leetcode.com/problems/binary-tree-maximum-path-sum/submissions/1485830381). TC: $$O(n)$$, SC: $$O(n)$$
* LC 543. Diameter of Binary Tree
  * [Optimal Answer](https://leetcode.com/problems/diameter-of-binary-tree/submissions/1493663948). TC: $$O(n)$$, SC: $$O(height)$$
* LC 129. Sum Root to Leaf Numbers
  * [Answer](https://leetcode.com/problems/sum-root-to-leaf-numbers/submissions/1800982394). TC: $$O(n)$$, SC: $$O(height)$$
    * The optimal answer is to use the **Morris Algorithm** with constant space, but I feel that's too complicated to write.

### **Construct Binary Tree (3)**

* Notes: Not difficult but easy to make mistakes in implementation
* :white\_circle: LC 106. Construct Binary Tree from Inorder and Postorder Traversal
  * [Optimal Answer](https://leetcode.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/submissions/1111036733/).  TC: $$O(n)$$, SC: $$O(n)$$
* :white\_circle: LC 105. Construct Binary Tree from Preorder and Inorder Traversal
  * [Optimal Answer](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/submissions/1799715008). TC: $$O(n)$$, SC: $$O(n)$$
* LC 654. Maximum Binary Tree
  * Approach 1 (Nonoptimal - Recursion): [Answer](https://leetcode.com/problems/maximum-binary-tree/submissions/1730548364/). TC: $$O(n^2)$$, SC: $$O(H)$$
  * :orange\_circle: Approach 2 (Optimal - Monotonic Stack): [Answer](https://leetcode.com/problems/maximum-binary-tree/submissions/1730564467/). TC: $$O(n)$$, SC: $$O(n)$$
    * ```
      Let me try to explain the algorithm.
      If we have built the max binary tree for nums[0] ~ nums[i - 1], how can we insert nums[i] to the binary tree?
      Say the max binary tree for nums[0] ~ nums[i - 1] looks like:

            A
           / \
        ...   B
             / \
          ...   C
               / \
            ...   ...
      Say the node for nums[i] is D.
      If D.val > A.val, then because A.val is at the left of D.val, we can just move the tree rooted at A to the left child of D.

              D
             /
            A
           / \
        ...   B
             / \
          ...   C
               / \
            ...   ...
      If D.val < A.val, then because D.val is at the right of A.val, D must be put into the right subtree of A.
      Similarly, if D.val < B.val, then D must be put into the right subtree of B.
      Say B.val > D.val > C.val, then D should be the right child of B. (because D.val is at the right of B.val, and D.val is the biggest among the numbers at the right of B.val.)
      Because C.val < D.val, and C.val is at the left of D.val, C should become left child of D.

            A
           / \
        ...   B
             / \
           ...  D
               /
              C
             / \
          ...   ...
      So to update the max binary tree for nums[0] ~ nums[i - 1], we need to know the nodes on the right path of the tree. (A, B, C, ...)
      How to maintain the path?
      Let's look at the properties of the nodes.
      A is the biggest among nums[0] ~ nums[i - 1].
      B is the biggest for the numbers between A and nums[i] (exclusive).
      C is the biggest for the numbers between B and nums[i] (exclusive).
      Let's use a stack, and assume that the content of the stack contains the "right path" of nodes before the node for the current number.
      For the node of the new number, we should remove the nodes in the stack which are smaller than the current number.
      So we pop the stack until the top element of the stack is greater than the current number.
      Then, add the node for the current number to the stack.
      ```

### **Tree Leaf (1)**

* LC 872. Leaf-Similar Trees
  * [Optimal Answer](https://leetcode.com/problems/leaf-similar-trees/submissions/1466093078). TC: $$O(n)$$, SC: $$O(n)$$

### **Tree Accumulation**

* :orange\_circle: LC 2872. Maximum Number of K-Divisible Components
  * [Optimal Answer](https://leetcode.com/problems/maximum-number-of-k-divisible-components/submissions/2012022305). TC: $$O(n)$$, SC; $$O(n)$$
* LC 2265. Count Nodes Equal to Average of Subtree
  * [Optimal Answer](https://leetcode.com/problems/binary-tree-paths/submissions/1729517750/). TC: $$O(n)$$, SC: $$O(n)$$
* LC 1339. Maximum Product of Splitted Binary Tree
  * Bonus point: Think how to do it without using `long`
  * [Optimal Answer](https://leetcode.com/problems/maximum-product-of-splitted-binary-tree/submissions/1991542167). TC: $$O(n)$$, SC: $$O(h)$$

### **BST (10)**

* Notes
  * :jigsaw: _**Pattern 1: Traverse BST with prev node in the recursive way**_ (**LC 98**, 530, 501)
  * :jigsaw: _**Pattern 2: Traverse BST with stack in the iterative way**_ (**LC 98**, 230)
* :star2: LC 700. Search in a Binary Search Tree
  * [Optimal Answer](https://leetcode.com/problems/search-in-a-binary-search-tree/submissions/1466848128). TC: $$O(height)$$, SC: $$O(height)$$
* LC 98. Validate Binary Search Tree
  * Method 1: Use an array to store all elements visited by inorder traversal. Then check if each element in the array is bigger than the previous one. Very easy but needs extra space
  * :thumbsup: Method 2: Do validation during **inorder traversal** with 2 pointers. 1 pointer points to the current node. Another pointer points to the previous node (based on in-order sequence). In this way, we can bypass that limitation issue. Be careful to **make that `prev` node a class variable** instead of a function argument! The `prev` node is very hard to update if we pass it through the function argument. [Optimal Answer](https://leetcode.com/problems/validate-binary-search-tree/submissions/1863609991). TC: $$O(n)$$, SC: $$O(h)$$
  * Method 3: Use range to validate left and right nodes. [Optimal Answer](https://leetcode.com/problems/validate-binary-search-tree/submissions/1863615993). TC: $$O(n)$$, SC: $$O(h)$$
* LC 530. Minimum Absolute Difference in BST
  * Similar to LC 98
  * [Optimal Answer](https://leetcode.com/problems/minimum-absolute-difference-in-bst/submissions/1806271700). TC: $$O(n)$$, SC: $$O(h)$$
* :orange\_circle: LC 501. Find Mode in Binary Search Tree
  * Need some code skills to resolve it in 1 traversal
  * Need to do inorder traversal with prev pointer
  * If `maxCount > count`, we must clear the result list. For example \[1, null, 2, 2], when we meet 1st element `2`, we will keep both `1` and `2` in the result list. Then when we meet 2nd element `2`, although `2` already in the result list, we still need to clear it due to the element `1`.
  * [Optimal Answer](https://leetcode.com/problems/find-mode-in-binary-search-tree/submissions/1734479982/). TC: $$O(n)$$, SC: $$O(h)$$
* :star2: :orange\_circle: LC 235. Lowest Common Ancestor of a Binary Search Tree
  * Assumptions: `p != q`, `p` and `q` will exist in the tree, All `Node.val` are unique.
  * It's very easy to **not fully** use the property of BST and miss best solution. The best solution is very short by fully using the property of BST!
  * [Recursive Answer](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/submissions/1418401332/). TC: $$O(n)$$, SC:  $$O(h)$$
* LC 701. Insert into a Binary Search Tree
  * Assumptions: It is guaranteed that the new value does not exist in the original BST.
  * It's very easy to resolve if you insert a node as a leaf node.
* :star2: LC 450. Delete Node in a BST
  * The logic is straightforward. 5 cases in total. The first 4 cases are actually similar. Most code is for handling the 5th case.
    * No `targetnode`
    * `targetNode.left == null && targetNode.right == null`
    * `targetNode.left != null && targetNode.right == null`
    * `targetNode.left == null && targetNode.right != null`
    * `targetNode.left != null && targetNode.right != null`
  * [Optimal Answer](https://leetcode.com/problems/delete-node-in-a-bst/submissions/1418418818). TC: $$O(height)$$, SC: $$O(height)$$
* :white\_circle: LC 669. Trim a Binary Search Tree
* LC 538. Convert BST to Greater Tree
  * Try to resolve it without a helper function
  * [Optimal Answer](https://leetcode.com/problems/convert-bst-to-greater-tree/submissions/1738832965/). TC: $$O(n)$$, SC: $$O(h)$$
* :white\_circle: LC 230. Kth Smallest Element in a BST
  * It's **important** to know both recursive and iterative ways.
  * Approach 1 using the recursive way
    * &#x20;[Optimal Answer](https://leetcode.com/problems/kth-smallest-element-in-a-bst/submissions/1806281011).
    * TC: $$O(h+k)$$. O(H) to reach the smallest node in the BST. O(k) to find the kth smallest from there, doing an inorder search.
    * SC: $$O(h)$$
  * Approach 2 using the iterative way:  [Optimal Answer](https://leetcode.com/problems/kth-smallest-element-in-a-bst/submissions/1863603982). TC: $$O(h+k)$$, SC: $$O(h)$$
