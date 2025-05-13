---
num: "Lecture 7"
desc: ""
ready: false
lecture_date: 2025-04-24 15:30:00.00-7:00
---

* [Slides folder]({{ site.slides_url }}){:target="_blank"}

---

---

## Recursion 

- Optional recursion homework to help you understand the call stack and how it works with recursion.
- Recursion is a function that calls itself over and over again.
- Used for problems that can be broken down into smaller, similar subproblems.
- Each call adds a frame to the call stack.
- A base case is essential to prevent infinite recursion.

## Big O-notation
- Always think about the worst-case when analyzing performance.
- Interpret break and return as potential early exits, but assume they don’t trigger unless guaranteed.
- Always test with large values like 5,000 or 1,000,000.
- Ask: "Does this function do more work with more input?"
- If yes → it's not constant.
- If runtime grows with input → measure how it grows (linear, quadratic, etc).


