---
num: "Lecture 4"
desc: "Designing Python Classes and Methods"
ready: false
lecture_date: 2025-04-15 15:30:00.00-7:00
---

* [Slides folder]({{ site.slides_url }}){:target="_blank"}

---

---

- Make sure you come to class to clarify any issues you have. You are welcome to ask for any examples you might need help with regarding the lab or homeworks.
- Remember that the cyber security topics are not included in the textbook.
- There will not be a guide before exams, coming to class and learning and practicing each day is your consistent review guide.

* Student Question: For the midterm will there be practice questions on paper available outside of labs and homework?
* Answer: I will consider doing that in week 3 or 4. In general, I dislike wasting paper so there will most likely be a digital handout. You can come to office hours and we can work through examples. 

* Student Question: Default python had built-in functions like `int()` but there are other functions  where you put an object name and then use a dot afterward. How are those different in creating a class?

Sometimes in default python, if we are converting a string to interger we use `int()` but there is also a way if we have the string object name of a string variable. Calling a method on a string object to convert it.


How are they defined when creating new class?

When we create our own class and define methods that are specific to that class, those methods are written inside the body of the class and can only be accessed through an object of that class using dot notation.

There is one method that we don't call the way it is written in our documentation. For example, if the class is creating a new movie what is method we are talking about and how are we calling it? The `__init__` (student answered) is our constructor, the only method we have defined in our class that we don't use the dot notation for. We just call it by using the name of the class and putting parentheses after. Anything the constructor needs we put into the arguments of that class.
Any methods that are defined for that class, we use the ddot notation.

There are functions like `len()` (length/size of the container) that are saying: "you give me a string or a list or a dict and I will tell you how many objects there are". These functions do not belong to any specific class.

We can overload certain functions and operators so they work with our custom classes. As long as the class defines the appropriate special methods, these functions will recognize and work with its objects.

---

**How to define a method of a class versus defining a function?**

A method is a function that is defined inside a class.

Functions don't neccesarily have to live in class, like we learned in cs8, you can write functions by themselves. All values that they need from the outside need to be provided as arguments.

A very specific fucntion that is defined for the class and uses the attributes of the class is called a method of that class. 
A method is a function that is defined for that class.
Methods always have `self` as the first parameter because it refers to the specific instance of the class that is calling the method. It is not provided as an argument into the function.

---

// defined a new student class to illustrate methods and accessing attributes

* How to get student 2 perm number?
* `student2.perm`

* Do I need anything after defining a class as `class Student`?
* Colon, student answered

* Student Question: What happens if we only give it one argument?
* Test it, practice! It will use the default value which we gave it, `None`. It will print out `None` for whatever paremeter you left out. When we have arguments, if we don't use the parameter names, python will go by the position of the argumetns and assign them in this way. In order for us the change this we need to clarify which parameter it should be connected to. 

---

* If I am trying to convert something into a string that is all the method needs to do. `to_string()` with parenthesis because it is a method. If we don't include them, python tells us the memory address of the method, but it does not give us an error.

* Overwrite default python behavior by defining `__str__(self)`

Use a debugging trick in f-strings, if you put equal `=` python will print name of attribute, the `=`, and then automatically include the value that corresponds to that variable. 


We are not overwriting the print, we are overwriting the method that takes the content of the data type and turning it to a string. 
We took the str function that is built into python and told it what we want it to do. 


* Student Question: Is that function inside the print function? 
When I give some object to the print function, it needs to be converted to a string. Then, it uses what the string method `__str__(self)` is supposed to do with that object and displays it to the user.

* Student Question: Is there anyway to make the function only accept perm numbers of a certain length?
We are in charge of the constructor. In the constructor we can include `if` statements to do so. Such as if this is None, return an error, or if there are not enough characters or illegal characters.

---

When we create an object that has multiple parts and we want to append that object to a list of things, how does Python interpret that? 
I created `student1` and `student2`, but now I want them to be grouped together. If I want a course that keeps track of a roster, those students are separate objects from the collection that tracks them. Course is a new class — a **composite class** — that holds these student objects. Now that this is stored in a dictionary, we need to know what the distinguishing key is when adding each student to the course.

If you have "jazz" mapped to a category key, will the song still know that it belongs to the jazz genre? Will the song still include both the title and the genre?
When I create a new song, does that song remember its genre? 

Yes — because of the way we set up the constructor with default values. Just by being an object of the Song class, it automatically gets those values. In order to construct the song object, it needs those two pieces of information — either you provide them when creating the song, or the constructor will use the default values we defined.

- What would happen if we didnt give it the objects?
- Create an empty object

If I remove the constructor completely, we haven’t overwritten the constructor; we’re just creating the object here. Python is looking at student1, and by default, it’s giving us that value — it's not defined yet. As soon as we decide to create our own class, that’s when we lose the ability to use the default constructor. If we didn’t provide those values in our class, Python wouldn’t know how to initialize the object.

* "Super student"

* What happens when we call `Student()` and put multiple parameters? Putting more into the function that python expects.

It will return a type error and say it only expected however many parameters.






