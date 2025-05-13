---
num: "Lecture 8"
desc: "Recursion review; Midterm notes"
ready: false
lecture_date: 2025-04-29 15:30:00.00-7:00
---

* [Slides folder]({{ site.slides_url }}){:target="_blank"}

---

---

# Midterm

- The midterm is next **Thursday, May 1st**.
- Study over the weekend for the midterm! 
- We will have a review in class next **Tuesday, April 29th**.
- Everything on the exam has been something we have seen or done in class, the homeworks, or the labs.
- Try to do practice problems on paper to simulate the same format of the exam. 

# The Three Laws of Recursion

### 1. The Function Must Have a Base Case
- A **base case** is the condition under which the recursion stops.
- The base sase is like a "Younger Sibling".
  - It knows how to do one simple task without needing recursion.
- The base case is the **simplest version** of the problem.
- The base case usually involves the simplest input, such as:
  - A number set to `0`
  - An empty list (`[]`)
  - An empty string (`""`)

### 2. The function should move toward the base case with every recursive call.
- This means the **parameters** passed into the function should change.
- The argument must get **closer and closer** to the base case.
- This _could_ involve:
  - **Subtracting** from a number
  - **Slicing** a list or string

### 3. The Function Must Call Itself
- Recursion involves the function making **a call to itself**.
- starts in one direction and makes copies of itself
- The function continues to call itself until the base case is met, then it starts to "unwind" itself by popping off the previous function calls from the call stack.
