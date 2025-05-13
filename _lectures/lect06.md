---
num: "Lecture 6"
desc: "Deriving Big-O and Algorithm Analysis, Recursion"
ready: false
lecture_date: 2025-04-22 15:30:00.00-7:00
---

* [Slides folder]({{ site.slides_url }}){:target="_blank"}

---

---

## Announcments 

- Last of the slower days. Hw01 and Lab01 are due tonight! Labs and homework are always due each week on Tuesday at midnight.

- The homeworks relate to the corresponding chapters and sections of the textbook that are explicitly stated on the lecture slides. 
- Electronic version is not the official version and sometimes crashes.

- The inheritance section of the textbook explains that it allows us to use the methods of a parents class.
- We need to visualize and understand where python will jump in its execution.

  
- While the fraction class is easy to understand, the example is slightly harder to understand if you do not run through the example yourself. 
- Try using [python tutor](https://pythontutor.com/render.html#mode=edit), it is highly recommended and very efficient. It allows you to walk through the steps one at a time and provides a visual as well. 

- Make sure you have a mental picture of what is going on with the 
- 
- code before you start coding.
- This will provide you with a much better understanding when jumping into the labs.


## iClicker Questions

- Any other attributes?
  - Perm number, distance from campus.


- What does it mean to have a standard method? 
  - `__str__` is a standard methods provided to you by python. 

- What would be a potential advantage of providing our own constructor?
  - Student jumping ahead: "It gives us control over how the object is initialized, and if another class inherits from it, the child class can also inherit that initialization."
  - Another student answered: "More convienet to initialize an object of that class with all of the attributes we have already defined."
  - When we have constructor, we are batch-creating all of the attruutes we want the object to have.
  - Creates a container that is consisent across all of the objects of that class.

- What does a getter method do?
  - Student answered: "Return the value of whatever it is in charge of getting."
- What input does it need?
  - No input is necesary, since it returns a value.


## Other Questions

- Will you post practice questions for the midterm?
  - (See previous lecture notes) The questions that I have at beginning of slides that we go over in class are the review questions. 


## Coding Example

- What does any method need as its first parameter?
  - `self`

- How do I represent the fact that I am comparing two objects?
  - Student answered: "You need the other object as an argument"

- Need to return the result that I am comparing?
  - Yes, the result of comparing two PERM numbers
 
- What other operators exist?
  - Addition
  - Comparison

- How do we compare two objects by the year instead?
  - Replace `name.upper` with year
  
- How do we compare two objects by the year _in addition to the name_?
  - Student answered: Use `(this == this) and (this == this)` meaning `return self.name == other.name and self.year == other.year`
  - `other` has to be an object of the same class or python will throw an attribute error
  - 







