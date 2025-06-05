---
num: "Lecture 18"
desc: "Final Exam Review Pt. 2"
ready: false
lecture_date: 2025-06-05 15:30:00.00-7:00
---

* [Slides folder]({{ site.slides_url }}){:target="_blank"}

---
# Exam Logistics

- **Date & Time**: Monday, June 9, 7:30 PM – 9:00 PM
- **Bring**: Pencils and an eraser (pens not recommended)
- **Instructions**:
  - Write neatly. If we cannot decipher what you wrote or if it looks like you selected more than one option, we will grade it as “incorrect”.
  - Have your student ID easily accessible.
  - Put away all electronic devices, papers, etc. Using them during the exam can result in receiving a 0 for the exam.
  - No bathroom breaks (unless arranged with a prof in advance due to a medical condition).
  - Be in class early. If you arrive late, after someone has already turned in their exam, you cannot take the exam and will receive a 0 for it.
  - When you turn in your exam:
    - Have your belongings with you
    - Show your ID when handing your exam

---

# What You Have (Hopefully) Gained From This Course

- Define custom Python objects and modules  
- Test your code automatically using Python  
- Implement object composition and inheritance  
- Implement custom data types (Stacks, Queues, Deques, Linked Lists, Ordered Linked Lists, Binary Trees)  
- Explain pros and cons of different implementations  
- Analyze running time of algorithms (Searching, Sorting, Storing, Retrieving)  
- Derive the Big-O notation to explain running time  

---

# 10-Week Journey  
TODO 

# Binary Tree vs. Heap (Binary Heap)

> **NOTE**: If we ask you to compare and contrast something on the exam, when you provide a trait, give a counterexample or counterpoint.

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
> It depends on where we're inserting and also how you implement the insert function. You could be adding at the root $O(1)$, or you could be adding into a balanced binary tree $O(\log n)$, or unbalanced binary tree $O(n)$. If you’re implementing the binary tree with a link to the last child, insertion would be $O(1)$ provided there is no ordering structure. In the case of a complete binary tree, this could be implemented with a Python list, and thus insertion would also be $O(1)$.

---

### Q: Do all cases of binary search tree deletion have the same O-notation?  
> Case 1: No children, how much work are we doing? $O(1)$ to delete it and $O(\log n)$ to find the node we want to delete.  
> Case 2: One child. $O(1)$ to delete, and $O(\log n)$ to find.  
> Case 3: Two children: $O(\log n)$

---

### Q: Why is a heap $O(\log n)$ for insertion and deletion?  
> Heaps are optimized to delete the smallest or largest value. They’re typically at the root of the tree, so this is done in $O(1)$ time. We need to maintain the heap property, so we take the last element and move it to where the root used to be, and if the property is broken, then you percolate it down. In the worst case, it goes from root to leaf, and there are $\log n$ levels to the tree, so it is $O(\log n)$.

---

### Q: Do we have to understand the hash and the map data types, but not how to implement it?  
> Yes, you have to understand the hash map data types, but you are not expected to know how to implement it.

---

### Q: What is the hash data type?  
> Hash data type is implemented using a hash function. The reason how the dictionary is able to retrieve data quickly is because of the hash data type. A sample implementation for a hash function is to use the size of my table as a modulo. It may come up on the final. It will come up if you’re comparing the Python list and dictionary. More on hashing [here](https://www.geeksforgeeks.org/introduction-to-hashing-2/)

---

### Q: Will there be anything that we have not implemented that shows up as a surprise on the exam?  
> Professor is not one for surprises, for example the practice exam is essentially the same format and same types of questions as the exam. TLDR: No, if there is, it will be a bonus question.

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
> Pay attention to the conditions closely such as break statements or returns.

---

### Q: If we have a return or a break, then we don’t multiply it in our calculation?  
> Yes, there is an early exit, so it is not included.

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
> Yes, don’t make your own assumptions, there will be more space on the exam for the questions to be more specific.

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
> Yes, it is possible, but it is more difficult and many more lines of code than the recursive solution. You have to keep track of where you are in the tree.

---

### Q: The solution isn’t using a getter, does that mean that the parent, left, and right attributes are in the same class?  
> This is the Node class, which contains references to parent, left, and right. The question on the exam will likely use getters.

---

### Q: Will we be provided with getters?  
> Assume they are implemented.
