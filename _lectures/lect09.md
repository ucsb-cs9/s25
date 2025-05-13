---
num: "Lecture 9"
desc: "Binary Search, Big-O, Dictionary vs List"
ready: false
lecture_date: 2025-05-06 15:30:00.00-7:00
---

* [Slides folder]({{ site.slides_url }}){:target="_blank"}

---

---

# Lecture 8

## Time Complexity: `O(n)`
- **O(n)** means the algorithm scales linearly with the number of elements.
- If there are `n` elements, the operation may take up to `n` steps in the worst case.

## List Operations
- `pop(0)` removes the first element of the list.
  - This is **O(n)** because all the remaining elements must be shifted one position to the left.
- Searching with `in`:
  - The list is scanned sequentially.
  - This is also **O(n)** in the worst case.

## Dictionary Operations
- Dictionaries use a **hash table**.
- When using the `in` operator on a dictionary:
  - The word is checked as a key.
  - It directly checks if the key exists and retrieves the value if it does.

## Binary Search (on Lists)
- Binary search is an efficient search algorithm with **O(log n)** time complexity.
- However, it only works on **sorted** lists.
- It repeatedly divides the search space in half (hence the `log n`).
- In the worst case:
  - Find the element at the very end of the search process, or determine the element is not found.

In-class demo with 8 students to illustrate that in the worst case, the function will need to be called only 3 times: log (base 2) of 8 is 3 (because 2^3 = 8).


