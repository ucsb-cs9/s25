---
num: "Lecture 12"
desc: ""
ready: false
lecture_date: 2025-05-15 15:30:00.00-7:00
---

* [Slides folder]({{ site.slides_url }}){:target="_blank"}

---

# Lecture 12

## Questions Asked Before Class

**Question:** What sorting method does Python use?  
**Answer:** Python uses a combination of merge sort and insertion sort, specifically an algorithm called Timsort with a Powersort merge policy.  
More info: [Timsort Wikipedia](https://en.wikipedia.org/wiki/Timsort)

**Question:** Can Big-O running times all be found in the textbook?  
**Answer:** Yes, all relevant complexities should be found in the textbook.

---

## Linked Lists

**Question:** Are the linked list node and linked list object like the BookCollection and BookCollectionNode in the lab?  
**Answer:** Yes, the lab was applying these concepts in a more specific context. The `BookCollection` class essentially held `BookCollectionNode` objects, similar to a linked list holding its nodes.

**Explanation:** A `LinkedList` does not have `set_data()` or `set_next()` methods because those attributes and methods belong to the nodes, not the list itself.

**Question:** In lab, we used a dictionary to index CVEs for fast lookup. With linked lists, we had to traverse the entire list. What are the tradeoffs?  
**Answer:** Dictionaries provide fast O(1) average-case lookup due to hashing, but they require keys to be immutable and memory to be contiguous. Linked lists allow for dynamic memory usage and can be more flexible in certain structural scenarios, like maintaining insertion order or frequent insertions/deletions.

## Adding Nodes to a Linked List

```python
def prepend(self, new_node):
    new_node.set_next(self.head)
    self.head = new_node
```

**Question:** Is it important to set the “next” attribute of the new node before making it the head?  
**Answer:** Yes, otherwise the rest of the linked list would be lost when the head is overwritten.

## Ordered vs Unordered Linked Lists

- Unordered: Nodes are inserted without concern for value order, typically at the start.
- Ordered: Nodes are inserted in a specific order and require comparison operations to find the correct position.

**Question:** Do visual representations of ordered and unordered linked lists differ?  
**Answer:** No, they look the same visually; the key difference lies in their methods.

## Removing Nodes from Linked Lists

**Question:** What were the different approaches for removing a node (like an author) in Lab 5?  
**Answer:** One method used a `previous` pointer that follows `current`. Another approach fixed `previous` at the node before the one to remove and did more relinking.

**Question:** Would those two approaches have different time complexities?  
**Answer:** No, both require O(n) time to find the node, plus a constant amount of work to remove it.

## Adding Node After the Head

```python
if previous is not None:
    temp.set_next(current)
    previous.set_next(temp)
```

**Question:** Can we swap nodes without using a temporary object?  
**Answer:** The temporary object (`temp`) is necessary to hold the new node we’re adding. It's not about swapping, but about preserving reference order.

---

## Merge Sort

[Visualization Tool](https://www.hackerearth.com/practice/algorithms/sorting/merge-sort/visualize/)

Merge Sort is a **divide and conquer** algorithm:
- Divide: Break the list into smaller sublists
- Conquer: Recursively sort the sublists
- Combine: Merge sorted sublists into the original list

We’ve also discussed Bubble, Selection, and Insertion Sort – all O(n²) algorithms. Merge Sort improves this to **O(n log n)**.

### Implementation

```python
def mergeSort(alist):
    if len(alist) > 1:
        mid = len(alist) // 2
        lefthalf = alist[:mid]
        righthalf = alist[mid:]

        mergeSort(lefthalf)
        mergeSort(righthalf)

        i = j = k = 0

        while i < len(lefthalf) and j < len(righthalf):
            if lefthalf[i] <= righthalf[j]:
                alist[k] = lefthalf[i]
                i += 1
            else:
                alist[k] = righthalf[j]
                j += 1
            k += 1

        while i < len(lefthalf):
            alist[k] = lefthalf[i]
            i += 1
            k += 1

        while j < len(righthalf):
            alist[k] = righthalf[j]
            j += 1
            k += 1
```

### What Are i, j, and k?

- `i`: Tracks the current index in the left sublist
- `j`: Tracks the current index in the right sublist
- `k`: Tracks the index in the merged list

### Time and Space Complexity

- **Time Complexity:** O(n log n) – The list is split log n times, and each level requires O(n) work to merge.
- **Space Complexity:** O(n) – Additional space is required for the temporary sublists.
**Question:** Is the base of the log in O(log n) equal to 2 because we split into two parts?  
**Answer:** Yes. The base of the logarithm reflects the number of partitions. If you split into 3 parts, it would be log base 3.

### Subtle Implementation Detail

- Our implementation always makes the right sublist "heavier" due to the way we split the list.

### Summary of Advantages and Disadvantages

**Advantages:**
- Stable sort
- Always O(n log n), even in the worst case
- Good for linked lists

**Disadvantages:**
- Requires O(n) additional memory
- Not in-place (unlike quicksort or insertion sort)

---
