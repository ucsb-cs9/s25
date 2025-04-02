---
layout: lab
num: lab00
ready: true
desc: "Python Review (strings, dictionaries, loops)"
assigned: 2024-04-01 11:00:00.00-7
due: 2024-04-08 23:59:59.59-7
---

# Introduction

As a new employee of SecureNet Consulting, your first task is to set up your workspace and learn how to submit your completed tasks for evaluation (grading).
Your work is evaluated by an autograder.
Fortunately, you can check your work locally (before turning it in) to ensure your code is robust.

As always, to understand the big picture of the assignment in front of you, you are expected to read all instructions from the beginning to the end _before_ you begin implementing any of them.


## Goals for this lab

By the time you have completed this lab, you should have:
* installed Python
* created and run Python code in IDLE (or another IDE of your choice)
* practiced important Python concepts
* submitted an assignment using the Gradescope system

## Python concepts to review

Many of the concepts are covered in Section 1.4 - Review of basic Python ([online section 1.8](https://runestone.academy/ns/books/published/pythonds/Introduction/GettingStartedwithData.html)). I also recommend [Chapters 1 through 6 from the "AUTOMATE THE BORING STUFF WITH PYTHON"](https://automatetheboringstuff.com/#toc).

To do this lab, you should be comfortable
* defining functions
* iterating over lists and string characters (using `for` loops)
* comparing conditions using `if` / `elif` / `else` statements
* using string's `.isupper()` / `.islower()` and `.upper()` / `.lower()` methods
* writing tests using `assert` statements
* debugging (or at least using `print()` statements to debug your code)

# Get setup with Gradescope

SecureNet Consulting employees are evaluated with quarterly reviews, which are the aggregate of more regular evaluations through Gradescope. Your quarterly review will be your final grade, which will reflect all your homework, quizzes, and lab assignments.
All these scores will be stored and provided via [Gradescope]({{ site.gradescope }}).


Gradescope trusts the identity vetting of Canvas, so you will be automatically added to Gradescope (using your **@umail.ucsb.edu** account) if you click on the Gradescope link on Canvas. Once Canvas authenticates you, you should be able to use the link from the website and go to Gradescope directly.
(If you are still running into issues, such as the page not loading, try to use a different browser.)

<!-- You should have received an email notification with instructions about logging into Gradescope. Once you follow the instructions to set your password, you should have access to our course on Gradescope. You should see "CMPSC 9" in your Winter 2024 courses. -->

The lab assignment "Lab00" should appear in your Gradescope dashboard in CMPSC 9.
You will submit your code for Lab00 using the instructions on this page.

As always in this class, you can submit your files as often as you'd like to Gradescope (we encourage you to submit your code often to back up your progress).


# Install Python on your computer

The instructions on installing Python on your computer can be found here:

<https://www.python.org/downloads/>

Follow the appropriate links to install Python for your computer.

<!--
# Lab Section Computers

We are offering in-person lab sections this quarter in SSMS 1301. These computers are Windows machines with Python 3+ already installed. **In general, it is acceptable to conduct your work on your own computer for this class.**

The workstations in SSMS 1301 **WILL NOT** save your work such that when you log in / log out. If you plan on using these machines to do your work, it is a good idea to create back up versions of your work in case you plan on working on your personal computer - uploading versions of your work on github or Gradescope is a great way to do this since you can download / upload your work on any computer. Instructions on creating a repository on github to store your work is at the bottom of these lab instructions.
-->

# Create your Lab00 directory

As an employee of SecureNet, it's important to be organized.
The best practice is to create a "`cs9`" folder that will contain subfolders for each lab.
Thus, for this lab, you would create a `cs9/lab00` folder on your computer
where you can save your file(s) and work in this directory for Lab00.
It is best to create a new folder for each lab assignment.

# Python code editor

A code editor that is integrated with the Python interpreter is often referred to as an integrated development environment (IDE).

When creating files to work with, you may use any editor of your choice. However, I recommend IDLE since this comes pre-installed with Python and the lab instructions will guide you through the process using IDLE (a program to create and run Python programs).
Additionally, since IDLE relies on your writing code yourself, it is a good editor to help you practice the concepts in this class without any AI assistance.

You can launch IDLE running Python 3+ as a Windows Application. On a Mac or Unix system, you can start IDLE by typing `idle3` in a terminal window
(a program that gives us access to the `command line` interface for the computer). You can access the terminal window by opening up a terminal window:

![terminal icon](https://ucsb-cs9.github.io/f23/lab/lab00/Terminal.png)

* A Terminal Window should pop up
* You can then open the IDLE program by typing `idle3`

If you are encountering any issues or need help, feel free to ask a TA / ULA for assistance when getting started.

# Create a new lab00.py file

Create a `lab00.py` file in your lab00 directory. This `lab00.py` file will contain the Python code you will submit for this lab assignment.

Steps for creating this new file with IDLE are:
* Open IDLE on your computer
* Go to "File" -> "New File", which will create an untitled file.
* Save this file by going to "File" -> "Save", which will prompt you to save this file in a specified location.
    * Name this file `lab00` (the file will automatically be saved as a `.py` file).
    * Save this file under your `cs9/lab00` directory that you created for this lab.

# Copy the following code template into `lab00.py` and complete the function definitions

As a newly hired security analyst, you are responsible for implementing three Python functions for this lab, which review some of the concepts covered in CS 8 and the readings in h00.
You will need to learn how to submit assignments and check your own work before you submit it for evaluation.

Assert statements are a quick way to do simple testing.
Note that several `assert` statements are included after each function definition.
The goal is to run your code such that these assert statements do not produce any errors and your code successfully finishes execution.

In Python, code is executed line-by-line from top to bottom. So if your code has an error and an `assert` statement doesn't pass, then you will see which `assert`
statement failed and execution will stop (no other statements after the error will be executed).

To run your `lab00.py` file in IDLE, go to "Run" -> "Run Module". This will execute the file you're working on and display the output in
in IDLE's Interactive Shell.

> Remember to configure IDLE to show line numbers - it will make debugging a lot easier (IDLE Settings -> `Shell/Ed`).
> You can enable line numbers by going to IDLE -> Settings and in the dialog box that opens up, clicking on the `Shell/Ed` tab and clicking on the checkmark `Show line numbers in new windows`.
> To see the line numbers, close the opened file and re-open it.
> Alternatively, you can select the `"Show Line Numbers"` option from the top `"Options"` menu.


Copy the following code into your `lab00.py` file and complete the function definitions according to the comments (remember to type your actual name on the first line):

```python
# Lab00, CS 9, [type your name here]

def found_in_list(list1, list2):
    ''' When analyzing potentially malicious network traffic, analysts often
    need to check if suspicious IP addresses or domains appear in known
    threat intelligence lists.
    This function takes two lists as its parameters (list1 and
    list2). Return True if each element in list1 exists in list2.
        Return False otherwise. If list1 contains no elements, return True.

    '''
    # COMPLETE FUNCTION DEFINITION HERE

assert found_in_list(["one",2], [0,"one",2,"three"]) == True
assert found_in_list([], [1,2,3,4]) == True
assert found_in_list(["192.68.35.33","128.66.3.48"], ["128.67.3.148"]) == False
assert found_in_list([1,2,3], [3,2,1]) == True

def alternate_case(text):
    ''' In cybersecurity, obfuscation techniques are common. Malware authors
    often use case alternation to evade simple string matching in security
    tools. Security analysts need to normalize text for proper analysis.

    This function takes a string parameter (text) and returns a new
        string that flips the case of each alpha character in the provided text.

    '''
    # COMPLETE FUNCTION DEFINITION HERE

assert alternate_case("") == ""
assert alternate_case("This is a Sentence") == "tHIS IS A sENTENCE"
assert alternate_case("CS9") == "cs9"
assert alternate_case("9.95") == "9.95"

def get_counts(text):
    ''' Character frequency analysis is crucial in cryptography and for detecting
    encoding anomalies in suspicious files or communications.

    This function takes a string parameter (text) and returns a dictionary
        type where each key in the dictionary is a unique upper-case character
        in `text` and its associated value is the number of occurrences of the
        unique character in text. Note that the unique characters should be case
        insensitive ("a" and "A" are considered the same and should be stored as
        "A" in the dictionary). Non-alpha characters (including whitespaces)
        and their occurrences should also be stored in the dictionary.
    '''
    # COMPLETE FUNCTION DEFINITION HERE

dict1 = get_counts("This is a Sentence")
assert dict1.get("S") == 3
assert dict1.get("P") == None
assert dict1.get("I") == 2
assert dict1.get(" ") == 3

dict2 = get_counts("Pi is Approximately 3.14159")
assert dict2.get("1") == 2
assert dict2.get("A") == 2
assert dict2.get("P") == 3
assert dict2.get(".") == 1
assert dict2.get(4) == None

def swap_key_val(database):
    """ In security operations, data often needs to be reorganized for different
    types of lookups or to create reverse mappings.

        The function expects a database to be a dictionary.
        Assuming that an input dictionary has unique values for each key,
        return a new dictionary with the keys and values swapped.
    """
    # COMPLETE FUNCTION DEFINITION HERE

weaknesses = {"CWE-20": "Improper Input Validation", "CWE-287": "Improper Authentication" }
reverse_weaknesses = swap_key_val(weaknesses)
assert reverse_weaknesses["Improper Authentication"] == "CWE-287"
```

> Note that since the `swap_key_val()` function is supposed to return a **new** dictionary, it means that the original `database` parameter should not be modified. _write an assertion that tests that the initial object is intact._ Ask for help if you are not sure how to structure such assert statement.


# Submitting to Gradescope

The lab assignment "Lab00" should appear in your Gradescope dashboard in CMPSC 9. If you haven’t submitted anything for this assignment yet,
Gradescope will prompt you to upload your files. This prompt is shown below:

![Gradescope_upload.png](https://ucsb-cs9.github.io/f23/lab/lab00/Gradescope_upload.png)

You either can navigate to your file(s) or "drag-and-drop" them into the "Submit Programming Assignment" window.

If you already submitted something on Gradescope, it will take you to their "Autograder Results" page.
There is a "Resubmit" button on the bottom right that will allow you to update the files for your submission.

For this lab, if everything is correct, you'll see a successful submission passing all of the autograder tests.

Note: Be sure to log out of the machine before you leave. In fact, you should do this every time you walk away from a lab computer.

# Troubleshooting

#### The autograder failed to execute correctly.

**Tip: Remove `print()` statements from your code**
if you see the following error message:

```The autograder failed to execute correctly. Please ensure that your submission is valid. Contact your course staff for help in debugging this issue. Make sure to include a link to this page so that they can help you most effectively.```

If the code contains `print()` statements when the Gradescope autograder does not expect to see anything printed, it fails the code with this message. In general, lab submissions do not require any `print` statements (though it may be helpful to use when debugging). If you see this error, remove any `print` statements in your code and resubmit it to Gradescope.

If the tests don't pass, you may get some error message that may or may not be obvious at this point. Don't worry - if the tests didn't pass, **carefully read the autograder message**, and take a minute to think about what may have caused the error. If your tests didn't pass and you're still not sure why you're getting the error, feel free to ask your TAs or Learning Assistants.


#### Assert statements

If you include assertions that don't pass in your code, then it is likely that none of the tests on Gradescope will pass.

You can try removing assert statements for the functions that you have not implemented yet, and see if you get credit for the tests that pass.

**Structure of an assert statement**

- Always start with the assert keyword
- Then, include an expression that involves the function that you are writing
  - Call the function using a specific input
- Use a comparison operator, typically `==` (but can also be others, for example `<` when comparing floats)
- Compare the returned value of the function with the result that you know the function is supposed to return

Example: `assert alternate_case("CS9") == "cs9"`
- after an `assert`, an expression that involves the function that you are writing is `alternate_case("CS9")`
  - it calls the function using a specific input `"CS9"`
- there is a comparison operator `==` to check that the function returned the exact value that we expect
- the returned value of the function that you know the function is supposed to return in this case is `"cs9"`
- if the `assert` evaluates to `True`, it passes; otherwise, it throws an `AssertionError`


#### EOF error

If you are getting an EOF error, check that you are not using `input()` anywhere in your code.
Parameters are passed directly into the function call, so there is no need for user input.


#### `ModuleNotFoundError: No module named ...`

Check that you named your file EXACTLY as was specified - remember that Python is case-sensitive, so **lab00.py** is not the same as **Lab00.py**.

---

As a SecureNet Consulting analyst, your careful attention to detail and ability to read, understand, and follow the instructions will allow you to minimize debugging time.

---

_Acknowledgment: This lab has been modified in collaboration with Noah Spahn to incorporate cybersecurity context._

