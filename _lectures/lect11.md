---
num: "Lecture 11"
desc: ""
ready: false
lecture_date: 2025-05-13 15:30:00.00-7:00
---

* [Slides folder]({{ site.slides_url }}){:target="_blank"}

---

---

# Sorting methods

## Bubble Sort

### Description

Bubble Sort is a comparison-based sorting algorithm. It works by repeatedly stepping through the list, comparing adjacent items, and swapping them if they are in the wrong order.

Each pass through the list places the next largest unsorted element in its correct position at the end. 

### Algorithm Steps

1. Starting from the beginning of the list, compare each pair of adjacent elements.
2. If the first is greater than the second, swap them.
3. Repeat the process for the entire list.
4. Continue making passes through the list until no swaps are needed.

### Python Implementation

```python
def bubbleSort(aList):
    for passnum in range(len(aList) - 1, 0, -1):
        for i in range(passnum):
            if aList[i] > aList[i + 1]:
                # Swap adjacent elements
                temp = aList[i]
                aList[i] = aList[i + 1]
                aList[i + 1] = temp

#Test cases
list1 = [1, 2, 3, 4, 5, 6]
list2 = [2, 2, 2, 2, 2, 2]
list3 = []
list4 = [6, 7, 5, 3, 1]

bubbleSort(list1)
assert list1 == [1, 2, 3, 4, 5, 6]

bubbleSort(list2)
assert list2 == [2, 2, 2, 2, 2, 2]

bubbleSort(list3)
assert list3 == []

bubbleSort(list4)
assert list4 == [1, 3, 5, 6, 7

### Time Complexity

Bubble Sort has a time complexity of **O(n²)** in the worst and average cases.

### Best Case

If the list is already sorted, Bubble Sort will still make all the comparisons unless we add an optimization to detect if no swaps were made during a pass.  
With that optimization, the best case becomes **O(n)**.

### Space Complexity

- **O(1)** — Bubble Sort sorts in-place without using extra memory.

### Summary

- Simple to implement  
- Inefficient on large lists  
- Can be optimized with early exit when no swaps occur during a pass

---

## Selection Sort

### Description

Selection Sort is another simple comparison-based sorting algorithm.  
Unlike Bubble Sort, which swaps adjacent elements repeatedly, Selection Sort finds the largest (or smallest) element and places it in its correct position with a single swap per pass.

### Algorithm Steps

1. Start at the beginning of the list.
2. Find the largest unsorted element.
3. Swap it with the last unsorted position.
4. Repeat for the remaining unsorted portion.

### Python Implementation

```python
def selectionSort(aList):
    for fillslot in range(len(aList) - 1, 0, -1):
        positionOfMax = 0
        for location in range(1, fillslot + 1):
            if aList[location] > aList[positionOfMax]:
                positionOfMax = location
        # Swap the maximum element into place
        temp = aList[fillslot]
        aList[fillslot] = aList[positionOfMax]
        aList[positionOfMax] = temp

#Test cases
list1 = [1, 2, 3, 4, 5, 6]
list2 = [2, 2, 2, 2, 2, 2]
list3 = []
list4 = [6, 7, 5, 3, 1]

selectionSort(list1)
assert list1 == [1, 2, 3, 4, 5, 6]

selectionSort(list2)
assert list2 == [2, 2, 2, 2, 2, 2]

selectionSort(list3)
assert list3 == []

selectionSort(list4)
assert list4 == [1, 3, 5, 6, 7]

### Time Complexity

Insertion Sort has a time complexity of **O(n²)** in the **worst and average cases**.  
This occurs when the list is in reverse order and every new element must be compared with all the previously sorted elements.

### Best Case

If the list is already sorted, each element is only compared once with its predecessor, resulting in a best-case time complexity of **O(n)**.

### Space Complexity

- **O(1)** — Insertion Sort is an in-place sorting algorithm and does not require additional memory.

### Summary

- Simple to implement  
- Efficient for small or nearly sorted datasets  
- Performs well on partially sorted lists  
- Inefficient on large or reverse-sorted lists due to quadratic time complexity

---

## Insertion Sort

### Description

Insertion Sort is a simple comparison-based sorting algorithm.  
It builds the final sorted list one item at a time by taking each element and inserting it into its proper position among the previously sorted elements.

Unlike Selection or Bubble Sort, it only shifts elements rather than swapping unnecessarily.

### Algorithm Steps

1. Start from the second element in the list.
2. Compare it with the elements before it.
3. Shift all larger elements one position to the right.
4. Insert the current element into the correct position.
5. Repeat until the entire list is sorted.

### Python Implementation

```python
def insertionSort(aList):
    for index in range(1, len(aList)):
        currentValue = aList[index]
        position = index

        while position > 0 and aList[position - 1] > currentValue:
            aList[position] = aList[position - 1]
            position = position - 1

        aList[position] = currentValue

# Test cases
list1 = [1, 2, 3, 4, 5, 6]
list2 = [2, 2, 2, 2, 2, 2]
list3 = []
list4 = [6, 7, 5, 3, 1]

insertionSort(list1)
assert list1 == [1, 2, 3, 4, 5, 6]

insertionSort(list2)
assert list2 == [2, 2, 2, 2, 2, 2]

insertionSort(list3)
assert list3 == []

insertionSort(list4)
assert list4 == [1, 3, 5, 6, 7]

### Time Complexity

Insertion Sort has a time complexity of **O(n²)** in the **worst and average cases**.  
This happens when the list is in reverse order, requiring each new element to be compared and shifted past all the previous ones.

### Best Case

If the list is already sorted, each element is simply compared once with its immediate predecessor.  
No shifting is needed, resulting in a best-case time complexity of **O(n)**.

### Space Complexity

- **O(1)** — Insertion Sort is an in-place sorting algorithm and requires no additional memory.

### Summary

- Simple to implement  
- Efficient for small or nearly sorted datasets  
- Performs well on partially sorted lists  
- Inefficient on large or reverse-sorted lists due to quadratic time complexity

---





