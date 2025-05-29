---
num: "Lecture 15"
desc: ""
ready: false
lecture_date: 2025-05-27 15:30:00.00-7:00
---

* [Slides folder]({{ site.slides_url }}){:target="_blank"}

---

---

## Lecture 15

**Announcements**
- There will be lab 10 which has a differnt format than the last labs. It is an implementation that is incomplete and it will be up to you to complete it. 
- Stay on the look out for extra credit opportunities!
- The final exam is on Monday, June 9th at 7:30 pm - 9:00 pm

## Binary Search Trees
- A binary tree is a tree data structure in which each node has at most two children, commonly referred to as the left child and right child.

Balanced Binary Tree:
- A balanced binary tree is a binary tree where the height (or depth) difference between the left and right subtrees of any node is at most one. This ensures that the tree remains approximately balanced, which helps maintain efficient performance for operations like insertion, deletion, and lookup.

Complete Binary Tree:
- A complete binary tree is a binary tree in which all levels are fully filled except possibly the last level, which is filled from left to right. This structure is often used in heap implementations.

# iClicker #1 
Does every node have at most two edges—one to its left child and one to its right child?

To determine if a binary tree is balanced, perform any tree traversal (such as in-order, pre-order, or post-order) to visit all the nodes. For each node, check whether the height difference between its left and right subtrees is at most 1.

It's important to note that if a tree is not balanced, it cannot be a complete binary tree. This is because a complete binary tree must be as compact as possible.

# iClicker #2
**Question:*** Can I compare the root node to the leftmost leaf node when checking if a tree is balanced?

**Answer:** No. When checking if a tree is balanced, you're comparing the height of the left and right subtrees of the same node, not one node to another. You do look at the height from the root down to the leaves, but balance is checked locally at each node. For completeness, the tree must be filled level by level from left to right. 

**Question:** Why wouldn't it be incomplete?

**Answer:** Because the correct term is “not complete,” not "incomplete." In binary tree terminology, we say a tree is complete or not complete, "incomplete" isn't typically used.

## Binary Trees vs. Binary Search Trees
**Question:** What do we do when we want to add an element to the tree? 

**Answer:** Replace it. Depending on how many items the tree has we can check if its an identical item and if not we can assume its an update and replace an item.

A Binary Search Tree is a binary tree where each node follows the **BST property**:
- Left subtree contains values less than the node’s value
- Right subtree contains values greater than the node’s value
- BSTs allow for efficient insertion, deletion, and lookup operations.
    - Average time complexity: O(log n), but can degrade to O(n) if unbalanced
    - Supports ordered data structure with dynamic updates

When analyzing if a tree is a binary search tree recal the heap order property. For every node, if its a max heap, every parents is greater than its children and vise versa for a min heap. 

# BST vs. Heap
What is the main difference between the BST and the heap?
- Heap is organized vertically by levels and we know the top of the heap is the very most important level for us, a binary search tree is orgnaized horizontally.
- The heap is guanteeed to be a completely balanced tree but the binary search tree is just a binary tree.
- How are the nodes stored?

## Map ADT
A Map Abstract Data Type (ADT) maps keys to corresponding values.

One common implementation is using a hash table, which uses a hash function to efficiently locate the value associated with a given key.

Disadvantage:
Hash tables can be memory-intensive because they store a bunch of keys to their corresponding values. They often allocate extra space to reduce collisions and store a large number of keys and values. 

## Inserting into a BST
**Question:** If we are filling in a binary search tree like we are filling in a heap, why is it not guanteed to have completeness? 

**Answer:** The way we are fiulling in the heap is left to right, making sure we maintain the heap order property. With this, we maintain binary search tree property which might cause lopsidedness. Whatever the first item you put in as the root will determine the rest of the tree.

**Question:** When inserting into a binary search tree, we insert at the top, but with heaps we insert at the bottom? 

**Answer:** In a Binary Search Tree, we start at the root and walk through the tree to find the correct position based on the BST property (left for smaller, right for larger). The new value is inserted as a leaf node. In a Heap, we always insert at the next available position to maintain completeness. After insertion, we percolate up to restore the heap property (min-heap or max-heap).

# iClicker 3
**Question:** Is this referring to the values in the tree inside or the way that it is structured? 

**Answer:** Is the way the tree is going to look like in the end going to change based on the way that I inserted?

**Question:** Why don’t we just build a balanced binary tree by picking the middle element from a list of numbers when constructing the tree?

**Answer:** We can do that if we know all the data in advance—this is a common way to build a perfectly balanced binary search tree. However, in live systems, we usually don’t know all the items ahead of time. Data arrives incrementally, and we insert values as they come in.
Because of this, the tree can become unbalanced, especially if values are inserted in sorted order. To handle this, data structures like Red-Black Trees are used—they rebalance themselves automatically after insertions and deletions to maintain efficiency. (Note: Not using in this class.) So, unless you have the full list of values beforehand, you can’t guarantee a balanced tree just by construction.

**Question:** What happens if we insert a repeated key into a binary search tree?

**Answer:** It depends on the application and how the tree is implemented.
Some systems might:
- Replace the existing value associated with the key (as the book suggests)
- Warn the user and ask whether to replace or ignore the duplicate
- Allow duplicates by modifying the structure (e.g., storing duplicates in a list or always inserting to one side)


