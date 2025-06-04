---
num: "Lecture 14"
desc: ""
ready: false
lecture_date: 2025-05-22 15:30:00.00-7:00
---

* [Slides folder]({{ site.slides_url }}){:target="_blank"}

---

---

Q: Do we check one node or all nodes to determine if a tree is balanced?

A: If you find any node where the left and right subtree heights differ by more than 1, that’s enough to say the tree is not balanced. If you can’t find such a node right away, scan through all of them and look for where the tree appears visually unbalanced.

---

Q: At one node, the left subtree has height 2 and the right has height 0. Is it unbalanced?

A: Yes, the difference is more than 1, so that node is unbalanced.

---

Q: Why is this not a complete tree?

A: In a complete tree, every level except possibly the last must be completely full. On the last level, all the nodes must be as far left as possible—meaning you can’t have a right child without having a left sibling.

---

Q: Do right siblings always need a left sibling in a complete tree?

A: Yes, a right child on the last level must have a left sibling for the tree to be complete.

---

Q: On the left-hand side, are we not comparing left and right?

A: When checking for balance, you compare the left and right subtrees of the node you’re focusing on. Nodes from separate subtrees shouldn't be directly compared when evaluating balance.

---

Q: What adjustment do we make when using a list to implement a heap?

A: We often set the first element of the list to None so that indexing starts at 1. This makes parent/child index calculations easier.

---

Q: Are we deleting the root node or any node in heap deletion?

A: In worst-case analysis, we assume deletion of the root node because it involves the most work.

---

Q: What happens when we delete the root of a heap?

A: The last node in the heap is moved to the root position, and then we heapify (percolate down) to restore the heap property.

---

Q: When not specified, should we assume a min heap or max heap?

A: If not told, do not assume. But in many CS classes, max heap is assumed by default unless otherwise specified.

---

Q: 50 is greater than 38 but is placed “incorrectly.” Does the tree still maintain the heap property?

A: Yes, if it’s a max heap, the parent should be greater than or equal to its children. As long as that condition holds, the heap property is maintained.

---

Q: Is it always the left or right child that is greater in a max heap?

A: Not necessarily. When restoring the heap property, you must compare both children and choose the larger one to maintain the max heap.

---

Q: If we’re not given the tree but just a list, how do we construct the tree?

A: You build the tree by filling it out level-by-level from left to right. This matches the order in which the list is structured in heap implementations.

---

Q: It’s hard to see where the subtree ends in the list—any tips?

A: Remember, for an element at index i in the list:
   - Its left child is at index 2i
   - Its right child is at index 2i + 1

---

Q: Are we assuming the tree is binary when using a list to represent it?

A: Yes, we always assume it’s a binary tree in these contexts (e.g., for heaps or binary trees in general).
