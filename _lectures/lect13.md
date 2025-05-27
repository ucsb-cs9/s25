---
num: "Lecture 13"
desc: ""
ready: false
lecture_date: 2025-05-20 15:30:00.00-7:00
---

* [Slides folder]({{ site.slides_url }}){:target="_blank"}

---

---

# Questions

Q: We will have until tomorrow to submit the lab?
A: Yes.

Q: How many edges can be going out of the node? 
A: As many as we want.

Q: How do we know when it is a completed tree?
A complete binary tree has all levels fully filled except possibly the last, which is filled from left to right without gaps. This structure allows efficient array-based implementation of heaps, which are used for priority queues, keeping operations like insert and delete at O(log n).

Q: If it is a balanced tree is it also complete? 
A: If its a complete tree, it always has to be balanced.

## Trees – Terminology

- **Node**: An element in the tree. May have one incoming edge and many outgoing edges.
- **Edge**: A connection between nodes (can be directional or bidirectional).
- **Root**: The top-most node (node without any incoming edges).
- **Path**: A sequence of nodes from one to another along the tree.
- **Children**: Nodes that have incoming edges from a parent node.
- **Parent**: A node with outgoing edges to its children.
- **Sibling**: Nodes that share the same parent.
- **Subtree**: A tree rooted at a child node of another tree.
- **Leaf**: A node without any outgoing edges.
- **Level**: Number of edges from the root node to a specific node.
- **Height**: Maximum level/depth of the entire tree.

---

## Priority Queues

- Similar to standard queues (FIFO), but with priorities.
- Elements are inserted with an associated priority.
- The element with the highest (or lowest) priority is dequeued first.
- Typically implemented using Heaps for efficiency.

---

## Tree Properties

- Binary Tree: Each node has at most two children.
- Balanced Binary Tree: Left and right subtrees of every node differ in height by at most 1.
- Complete Binary Tree: Every level, except possibly the last, is fully filled. Last level is filled left to right.

---

## Heaps

### MaxHeap
- A complete binary tree where every parent node is greater than or equal to its children.
- Used to implement a priority queue where the max element is always at the root.

### MinHeap
- A complete binary tree where every parent node is less than or equal to its children.
- Used to implement a priority queue where the min element is always at the root.

### Heap Representation in Python
- Represented as a list where index `0` is unused.
- Relationships:
  - **Parent**: `index // 2`
  - **Left child**: `2 * index`
  - **Right child**: `2 * index + 1`

---

## MaxHeap Insertion (Algorithm)
1. Insert the new element at the next available position.
2. While the element is greater than its parent:
   - Swap the element with its parent.
3. Time complexity: **O(log n)**

---

## MaxHeap Deletion (Removing Max)
1. Save the root value.
2. Move the last element to the root.
3. While the new root is smaller than one of its children:
   - Swap with the larger child.
4. Time complexity: **O(log n)**

---

## MinHeap Implementation (from textbook)

```python
# MinHeap
class BinHeap:
    def __init__(self):
        self.heapList = [0]
        self.currentSize = 0

    def percUp(self, i):
        while i // 2 > 0:
            if self.heapList[i] < self.heapList[i // 2]:
                tmp = self.heapList[i // 2]
                self.heapList[i // 2] = self.heapList[i]
                self.heapList[i] = tmp
            i = i // 2

    def insert(self, k):
        self.heapList.append(k)
        self.currentSize += 1
        self.percUp(self.currentSize)

    def percDown(self, i):
        while (i * 2) <= self.currentSize:
            mc = self.minChild(i)
            if self.heapList[i] > self.heapList[mc]:
                tmp = self.heapList[i]
                self.heapList[i] = self.heapList[mc]
                self.heapList[mc] = tmp
            i = mc

    def minChild(self, i):
        if i * 2 + 1 > self.currentSize:
            return i * 2
        else:
            if self.heapList[i * 2] < self.heapList[i * 2 + 1]:
                return i * 2
            else:
                return i * 2 + 1

    def delMin(self):
        retval = self.heapList[1]
        self.heapList[1] = self.heapList[self.currentSize]
        self.currentSize -= 1
        self.heapList.pop()
        self.percDown(1)
        return retval

def test_BinHeap():
    bh = BinHeap()
    bh.insert(5)
    bh.insert(7)
    bh.insert(3)
    bh.insert(11)
    assert bh.delMin() == 3
    assert bh.delMin() == 5
    assert bh.delMin() == 7
    assert bh.delMin() == 11
