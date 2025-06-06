---
num: "Lecture 18"
desc: "Final Exam Review Pt. 2"
ready: false
lecture_date: 2025-06-05 15:30:00.00-7:00
---

* [Slides folder]({{ site.slides_url }}){:target="_blank"}

---
# Binary Tree vs. Heap (Binary Heap)

**NOTE**: If we ask you to compare and contrast something on the exam, when you provide a trait, give a counterexample or counterpoint.

## Structure
- A binary tree is a general data structure where each node has at most two children. Uses nodes and links.  
- A heap is a specialized type of binary tree that is always a complete binary tree. This means all levels are fully filled except possibly the last, which is filled from left to right. Uses nodes and links if implemented as a complete binary tree; can also be implemented using a list.

## Purpose
- Binary trees serve as a foundation for more specialized structures, such as binary search trees (BSTs) and heaps.  
- Heaps are commonly used to implement priority queues, where quick access to the maximum or minimum element is required.

## Ordering
- Binary tree does not enforce any specific ordering or structural property by itself.  
- Heaps enforce the heap property: in a max-heap, every parent node is greater than or equal to its children; in a min-heap, every parent node is less than or equal to its children. Heaps do not require any specific ordering between sibling nodes or between subtrees, only between parent and immediate children.

## Retrieval
- A binary tree is not optimized for any specific type of retrieval.  
- A heap is optimized to retrieve a min/max element (depending on the type of heap). Not optimized for a general retrieval of arbitrary items.

## Insertion/Deletion
- A binary tree is $O(n)$ for deletion because in the worst case the tree is skewed and we have to traverse almost all elements to insert or delete an item. Insertion depends on the application.
- A heap is $O(\log n)$ for insert and delete

---

### Q: What does it mean when "insertion depends on the application" in binary trees?  
> It depends on where and how you insert. If inserting at the root, it's $O(1)$. In a balanced tree, it’s $O(\log n)$; in a skewed tree, $O(n)$. Some implementations (e.g., complete binary tree via list) allow $O(1)$ insertion without ordering.

---

### Q: Do all cases of binary search tree deletion have the same O-notation?  
> - 0 children: $O(1)$ to delete, $O(\log n)$ to find.
> - 1 child: $O(1)$ to delete, $O(\log n)$ to find.
> - 2 children: $O(\log n)$ due to successor swap

---

### Q: Why is a heap $O(\log n)$ for insertion and deletion?  
> Insertions bubble up and deletions bubble down the tree to maintain the heap property. Both may traverse from root to leaf, which is $O(\log n)$.

---

### Q: Do we have to understand the hash and the map data types, but not how to implement it?  
> Yes, understand how they work and their efficiency, but no need to write the implementation.

---

### Q: What is the hash data type?  
> A hash table uses a hash function to map keys to indices for fast lookup. Python dictionaries use this. Example: `hash(key) % table_size`. More on hashing [here](https://www.geeksforgeeks.org/introduction-to-hashing-2/)

---

### Q: Will there be anything that we have not implemented that shows up as a surprise on the exam?  
> No. The exam matches the practice exam format. If anything new appears, it’ll be a bonus.

---

# Derive the Order of Magnitude (Big-O)

See more [here](https://drive.google.com/file/d/122fKbFEMSiLkqIS05fmNVZYnd03r8ebh/view?usp=sharing): lecture 6

- For any loop: note the maximum number of its iterations  
- A single loop over $N$ elements: $O(N)$  
- Two nested loops over $N$ elements each: $O(N^2)$  
- Three nested loops over $N$ elements each: $O(N^3)$  
- A loop that is independent of the number of elements runs in constant time: $O(1)$  
- A loop that discards about half of its input on each iteration runs in logarithmic time: $O(\log n)$  
  - **NOTE**: the division has to occur in every iteration for it to be $O(\log n)$  

---

### Q: What if I have nested loops, but they all depend on the same n?  
> Check the loop conditions—`break` or `return` might reduce iterations. Don’t assume worst-case without analyzing logic.

---

### Q: If we have a return or a break, then we don’t multiply it in our calculation?  
> Correct. Early exits mean the loop may not fully run, so don't multiply blindly.

---

# iClicker Questions

The accuracy on these questions today may help boost final exam grade  
See full questions and answer options, as well as explanations for the answers [here]()

- What is the order of magnitude of this algorithm?  
  - $O(n)$  
- What is the order of magnitude of this algorithm?  
  - $O(n)$, $100 \cdot n = 100n$  
- In an ordered linked list, what is the time complexity for inserting an item at the start of it?  
  - $O(1)$  

---

### Q: Are assumptions going to be stated on the exam?  
> Yes. Don’t assume anything not clearly specified; questions will be explicit.

---

- What is the worst-case time complexity of binary search? Assume a sorted list of $n$ elements.  
  - $O(\log n)$  
- What is the worst-case time complexity of QuickSort?  
  - $O(n^2)$  
- What is the worst-case time complexity of insertion sort?  
  - $O(n^2)$  
- What is the worst-case time complexity of the splitting step of merge sort?  
  - $O(\log n)$  

---

Write a recursive function `preorder_traversal(root)` that takes the root of a binary tree and returns a Python list of values in preorder traversal order

---

### Q: Can we implement it non recursively?  
> Yes, but it’s more complex. You’d need to simulate the call stack manually using a real stack.

---

### Q: The solution isn’t using a getter, does that mean that the parent, left, and right attributes are in the same class?  
> Yes. They're direct attributes of the Node class. On the exam, expect to use getters.

---

### Q: Will we be provided with getters?  
> Yes, assume getters are available.
