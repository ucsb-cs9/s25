---
num: "Lecture 17"
desc: "Final Exam Review Pt. 1"
ready: false
lecture_date: 2025-06-03 15:30:00.00-7:00
---

* [Slides folder]({{ site.slides_url }}){:target="_blank"}

---
# Lecture 17

## Autograder Issues

### What does "failed to run" mean?
This typically means there's a `print` statement in your code that's interfering with the autograder. These statements can break the expected output format, so make sure to remove or comment them out before submission.

### Does the autograder care if you use recursion or a stack?
- The autograder does **not explicitly check** whether you use recursion or a stack.
- However, using a **stack** could cause a **timeout** if the implementation isn't efficient.
- For **traversal methods**, you should:
  - Use the **getters and setters** in your class implementation to access and manipulate nodes.
  - Write **recursive helper functions** for operations like deletion or traversal.
  - Follow convention by prefixing recursive helper functions with an **underscore** (e.g., `_delete_node`).

---

## Group Activity: Comparing Data Structures & Sorting Algorithms

### Purpose
This activity encourages networking: connect with someone you haven't worked with before.

### Instructions
- Partner with someone **new**.
- Exchange **emails** for future collaboration. You will work with the same person on Thursday!
- If any questions arise, post them to the Gradescope assignment:  
  **“S25 Final Exam Prep.”**

### Reference
Check **slides 7 and 8** from last week's lecture notes:  
[View Lecture Notes on Google Drive](https://drive.google.com/file/d/1C9msh9carP1cyZsWdT3upVVjyw5l3YjP/view?usp=sharing)

---
