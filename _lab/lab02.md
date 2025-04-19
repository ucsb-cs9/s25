---
layout: lab
num: lab02
ready: true
desc: "Protocol Testing - Inheritance"
assigned: 2024-04-15 11:00:00.00-7
due: 2024-04-22 23:59:59.59-7
---

# Building a Security Protocol Testing Framework

## Background

### Why Security Protocols Matter

In today's interconnected world, our digital lives—from banking to healthcare to social connections—depend on secure systems. Security protocols are the "guardrails" that protect our sensitive information from malicious actors. When you make an online purchase, check your medical records, or simply log into social media, multiple security protocols work behind the scenes to verify your identity and protect your data.

As cyber threats continue to evolve in sophistication, organizations need robust security frameworks that combine different types of protection. Just as a bank uses multiple security measures (guards, cameras, vaults), digital systems require layered security protocols working together. In this lab, you'll build a simplified model of how security professionals design these integrated protection systems, giving you insight into how the digital world keeps our information safe.

### Understanding Protocol Cost

In cybersecurity, implementing stronger security protocols typically requires more computational resources. The `cost` attribute in our framework represents this computational overhead:

- **What is cost?** Cost measures the computing resources (processing power, memory, time) required to run a security protocol. Higher security generally demands higher computational cost.

- **Why does cost matter?** Organizations must balance security needs against available resources. A military-grade encryption protocol might provide excellent security but could slow down a system if implemented everywhere. Understanding the cost helps security architects make appropriate trade-offs.

- **Real-world example:** A fingerprint authentication might be more secure than a password but requires specialized hardware and more processing power to analyze biometric data, representing a higher "cost" despite better security.

In this lab, we measure cost in abstract "cost units" to simulate how security professionals evaluate the resource requirements of different protection mechanisms.


# Learning Goals

In this lab, you will create a Security Protocol Testing Framework by utilizing inheritance functionality and defining various Protocol objects and their properties. You'll have the opportunity to practice:
- Defining a base class and creating an inheritance hierarchy
- Defining derived classes and inheriting data and reusing functionality from a base class
- Overriding inherited methods from the parent class in the derived classes
- Installing pytest and unit testing your code

Note: In general, it is always important to work on labs and reading early so you can gain the proper context and utilize our office hours to seek assistance / ask clarifying questions during the weekdays before the deadline if needed!

It may be a good idea to read up on some concepts we’ll be using in this lab before you get started, specifically **Chapter 1.4.6.2 (Inheritance)**.


# Testing your code

## Step 1: Installing pytest

For this step, you will need to use the program called **Terminal** (on MacOS) or **Command Prompt** (on Windows).
Pytest will need to be installed on your computer since it does not come with Python by default. 


In most cases, pytest installation is identical across macOS and Windows if Python and pip are properly installed. 

1. Check your Python and pip versions:

    ```python --version```
    ```pip --version```
    
    If you're using Python 3 and those commands don't work, try:

    ```python3 --version```
    ```pip3 --version```
    
2.  Install pytest:

   ```pip install pytest```
   Or, if you're using Python 3:
   ```pip3 install pytest```

3. (Optional) Upgrade pip if needed:

   ```pip install --upgrade pip```
   OR
   ```pip3 install --upgrade pip```


If you successfully installed pytest, jump to Step 2; otherwise, if the above steps didn't work, here are additional links for reference:

* **Installation Guide**: https://docs.pytest.org/en/stable/getting-started.html
* **Windows Installation Guide** (created by previous Learning Assistants): Python and [Pytest Installation Guide for Windows](https://drive.google.com/file/d/1nPCwIA8cBAkiJ-kOKZFjkOskD94jmWYn/view)

IMPORTANT: when installing Python on Windows, make sure to **select the checkbox to Add Python 3.x to PATH!** If you have installed Python on your Windows machine already without selecting Add Python 3.x to PATH, the easiest thing to do is uninstall / reinstall Python and be sure to select this box.

Note: on MacOS running Python3, in the Terminal, try using `pip3` instead of `pip` if your installation is not working. If you are running into an error about pip upgrade, remember that you might need to use the `pip3` to do that: `pip3 install --upgrade pip`



## Step 2: Create testFile.py

In your `lab02` folder, create a file that will contain the tests for the classes from this lab and their corresponding methods.

Following the Test-Driven Development (TDD), for every class that you’ll write in its own file, you will create a corresponding Test class in the `testFile.py`. Each Test class must contain `test_` functions for the corresponding methods of that class (see examples below).

Your testFile will have 2 parts:
1. the `import` statements at the top of the file (one for each class; `from [filename] import [classname]` (substituting the correct filename and classname, which are usually the same)
2. the Test classes with their functions.

At the moment, your testFile.py should be empty, saved in the lab02 folder where you will create the files for the class definitions for this lab.


## Step 3: run testFile.py using pytest

Your next task is to locate your `lab02` folder using the Terminal (on MacOS) or Command Prompt (on Windows). These two programs give us access to command line - an interface that allows us to run commands that interact with the operating system (OS).

There are 2 things you need to do to run a testFile: navigation and execution.


### Step 3.1: Navigating to the correct folder on the command Line

**Why do we need to use `cd`?**
The `cd` command (short for **change directory**) is used to **tell your computer where to look for the files** you're trying to run. When you use `pytest`, it needs to know where your `testFile.py` and class files like `Protocol.py` are located. If you're not in the correct folder, Python won't be able to find these files, and you'll get errors like `ModuleNotFoundError`.

Navigation: To run pytests, you will need to "open" your lab02 folder (also referred to as "directory") on the command line.

In order to run your pytests, you can navigate to your folder where your lab02 code is located using the command line interface.

If you are familiar with the Unix `cd` command: open the command line and `cd` (change directory) to the lab folder.

If you are not familiar with the `cd` command: 
- If you are using macOS:
  - copy the path to the folder that contains testFile.py (holding the ALT key as shown here: https://apple.stackexchange.com/questions/317992/is-there-any-way-to-get-the-path-of-a-folder-in-macos)
  - open the command line (the Terminal program)
  - type `cd`, type a space, and then paste the path that you copied.
    - For example, your command could look like `cd /Users/YKK/Documents/cs9/lab02`
    - If any folder name in this path includes spaces in its name (e.g., “CS 9” instead of “CS9”), then make sure to add quotation marks around it (e.g., `cd "/Users/YKK/Documents/CS 9/lab 02"`)
    - If you copied the pathname to the testFile.py file (instead of its folder), then just delete that file name, leaving the rest of the path
  - press enter/return on the keyboard to run this command
- If you are using Windows: [Windows 10 How to Open Command Prompt in Current Folder or Directory](https://www.youtube.com/watch?v=bgSSJQolR0E) (a 1min YouTube video)


### Step 3.2: Executing testFile.py

Execution: After you open the terminal and navigate to the lab folder following the steps above, type the following command to run testFile.py using pytest.

On Mac:
```python3 -m pytest testFile.py```


On Windows:
```python -m pytest testFile.py```


If you see something like this, congratulations! You successfully installed and ran pytest.

```bash
=================== test session starts ====================
platform darwin -- Python 3.8.0, pytest-5.3.1, py-1.8.0, pluggy-0.13.1
rootdir: THE FOLDER YOU COPIED
collected 0 items

================== no tests ran in 0.01s ===================
```

If you run into any difficulties when installing / running pytest, and/or have any questions about testing your code, we will be happy to help you out during our office / lab hours!


## Step 4: understand pytest output messages

See Step 4 in the [Step-by-step instructions for using pytest](https://docs.google.com/document/d/e/2PACX-1vTbIEpAAAYTNv-zOMx5EP5bdbw-89na8jDUlQ45DBI8q8woNr41ho_DD6a9GPJlSB1SNUpjKrLlRTGK/pub) (some of them are included below as well).


---


# Lab Instructions

In this lab, you will create a `Protocol` **base class** as well as defining specific classes for a couple types of Protocols (Encryption and Authentication). The `SecuritySuite` class will organize Protocols and will provide a summary of a specific security suite.

In addition to defining classes for various Protocols and a Security Suite, you will test your code for correctness by unit testing various scenarios using pytest.
You will need to create five files:

1. `Protocol.py` - file containing a class definition with attributes all Protocols have.
2. `Encryption.py` - file containing a class definition of an encryption protocol that inherits from the Protocol class.
3. `Authentication.py` - file containing a class definition of an authentication protocol that inherits from the Protocol class.
4. `SecuritySuite.py` - file containing a class definition of a security suite containing various protocols.
5. `testFile.py` - file containing pytest functions testing the Protocol, Encryption, Authentication, and SecuritySuite classes.

To help you organize your code and use it for reference in future labs, we will provide you with a template code for the Protocol class, so that you can model the other classes accordingly.

For testing, you will create the `TestProtocol` class in the `testFile.py`, so that you can write the tests as you are implementing the class and its methods.


## Protocol class

The `Protocol.py` file will contain the class definition of a general security protocol.
We will define this class' attributes as follows:

- level - a string that represents the security level of the protocol ('basic', 'enhanced', 'military').
- cost - a positive float that represents the computational cost of the protocol.

You should write a constructor that passes in values for all the fields. You may assume that calls to the constructor will always contain a non-empty string representing the protocol's level and a positive float representing the protocol's cost.

```
__init__(self, level, cost)
```

In addition to your constructor, your class definition should also support "setter" and "getter" methods that can update and retrieve the state of the Protocol objects:

- `get_level(self)` - returns the level of the protocol
- `get_cost(self)` - returns the cost of the protocol
- `update_level(self, new_level)` - updates the level of the protocol
- `update_cost(self, new_cost)` - updates the cost of the protocol

Each Protocol object should be able to call a method `info(self)` that you will implement, which returns a string with the current protocol's level and cost. Since there are many protocols, the following output represents what will be returned if we call the info method after constructing a Protocol object:

```
proto1 = Protocol('enhanced', 20.5)
print(proto1.info())
```

Output:

```enhanced: 20.50 cost units```

Note: The `proto1.info()` return value in the example above does not contain a newline character (`\n`) at the end.

<!--Note: The quotation marks around the returned string in IDLE tell us that the value was returned, not printed, hence the string representation is shown.-->

Hint: Note that the return string should contain a cost with two decimal places. Use the f-string to show the floating point values with 2 decimal places. For example:
```
>>> cost = 5
>>> f"{cost:.2f}"
'5.00'
```

### Template for the Protocol and TestProtocol classes

Below is the skeleton template for the Protocol class that you can use as a starting point for your `Protocol.py` file:

```
# Protocol.py

class Protocol:
    def __init__(self):
        pass

    def get_level(self):
        pass

    def get_cost(self):
        pass

    def update_level(self):
        pass

    def update_cost(self):
        pass

    def info(self):
        pass
```

Immediately, we can add the corresponding test class and its testing methods to the testFile.py like so:

```
# testFile.py

from Protocol import Protocol

class TestProtocol:
    def test_init(self):
        pass

    def test_get_level(self):
        pass

    def test_get_cost(self):
        pass

    def test_update_level(self):
        pass

    def test_update_cost(self):
        pass

    def test_info(self):
        pass
```

The way the TestProtocol template was created:

1. copy the stubs for the Protocol class directly
1. add the corresponding `import` statement at the top of the file
1. change the name of the class from `Protocol` to `TestProtocol`
1. change the `__init__` method to be `test_init`
1. prepend `test_` to all the other methods


### Write tests for the TestProtocol class

Now, inside each test function in `testFile.py`, we test each class' methods using `assert` statements.

- If the method has a return value, directly assert the return value to verify its correctness;
- If the method doesn't have a return value, combine it with another method that has a return value to do the testing or assert that the object was modified correctly.

For example, we can use the example that we saw above, to create a sample Protocol object and test that it was correctly created:

```
from Protocol import Protocol

class TestProtocol:
    def test_init(self):
        protocol = Protocol('enhanced', 20.5)
        assert protocol.level == 'enhanced'
        assert protocol.cost == 20.5
```

Continue in this way to test the rest of the methods of the class:

```
def test_get_level(self):
    protocol = Protocol('military', 20.95)
    assert protocol.get_level() == 'military'
```

Before submitting your code to Gradescope, run your testFile.py using pytest to verify that all your tests are correct and are passing.
You are now ready to implement the rest of the classes and add their tests to testFile.py.

---

## Encryption class

The `Encryption.py` file will contain the class definition of an encryption protocol. Since an encryption is a protocol (i.e., IS-A relationship between classes), it should inherit the attributes we defined in the `Protocol` class.

HINT: Think of the `super` keyword discussed in the lecture. 

Your `Encryption` class definition should support the following constructor and method:

- `__init__(self, level, cost, algorithm)` - constructor that extends the parent class' (`Protocol`) constructor and sets the encryption algorithm (for example, "AES", "RSA", "Blowfish", etc.) as an attribute to the Encryption class.
  - Note, you may assume the algorithm parameter is a str.
  - In order to avoid code duplication, you must explicitly utilize the base class' constructor to set the level and cost attributes.
- `info(self)` - method should override the inherited `info()` method in the Protocol class, and returns a str with the properties of an Encryption object.
  - In order to avoid code duplication, you must explicitly utilize the base class' `info()` method to construct the Encryption object's information.
- `get_algorithm(self)` - returns the algorithm of the encryption.
- `update_algorithm(self, new_algorithm)` - updates the encryption algorithm of the Encryption object.


An example of what the return string format of the `info()` method is shown below:

```
>>> protocol2 = Encryption('basic', 3.0, "AES")
>>> protocol2.info()
'AES Encryption, basic: 3.00 cost units'
```

Note: The `protocol2.info()` return value in the example above does not contain a newline character (`\n`) at the end.

Note: The quotation marks around the returned string in IDLE tell us that the string value was returned, not printed, hence the string representation is shown.

---

## Authentication class

The `Authentication.py` file will contain the class definition of what an authentication protocol. Since an authentication IS-A protocol, it should inherit the attributes we defined in the `Protocol` class.

Your `Authentication` class definition should support the following constructor and method:

- `__init__(self, level, cost, factors)` - constructor that extends the parent class' (`Protocol`) constructor and sets a list of authentication factors used in this authentication object.
  - Note, you may assume the factors parameter is a list of strings representing the types of factors (for example, "password", "fingerprint", "facial", etc.) used in the authentication.
  - In order to avoid code duplication, you must explicitly utilize the base class' constructor to set the level and cost attributes.
- `info(self)` - method that overrides the inherited info method in the Protocol class, and returns a str with the properties of an Authentication object.
  - In order to avoid code duplication, you must explicitly utilize the base class `info()` method to construct the Authentication object's information.
- `get_factors(self)` - returns the factors of the authentication.
- `update_factors(self, new_factors)` - updates the list with the factors of the authentication.

An example of what the return string format of the info method is shown below:

```
>>> auth1 = Authentication('military', 8.5, ["Password", "Fingerprint"])
>>> auth1.info()
'Password/Fingerprint Authentication, military: 8.50 cost units'
```
Note: The `auth1.info()` return value in the example above does not contain a newline character (`\n`) at the end.

Note: The quotation marks around the returned string in IDLE tell us that the value was returned, not printed, hence the string representation is shown.

---

## SecuritySuite class

The `SecuritySuite.py` file will contain the class definition of what a security suite will contain, along with the total cost of all protocols in the security suite.

Your `SecuritySuite` class definition should support the following constructor and methods:

- `__init__(self)` - constructor that initializes an empty list to the class. Name this list attribute `protocols`. This list protocols will eventually expand with protocols for the security suite.
- `add(self, protocol)` - method that will add the protocol parameter to the SecuritySuite's list. The most recently added protocol will be at the end of the list. You may assume the protocol parameter will either be an Encryption or Authentication object.
- `total(self)` - method that will return a str containing each protocol in the security suite, and the total cost of all protocols in the security suite.

An example of what the return string format of the total method is shown below:

```
protocol1 = Encryption('basic', 3.0, "AES")
auth1 = Authentication('military', 8.5, ["Password", "Fingerprint"])
suite = SecuritySuite()
suite.add(protocol1)
suite.add(auth1)
print(suite.total())
```

Output:
```
Suite Components:
* AES Encryption, basic: 3.00 cost units
* Password/Fingerprint Authentication, military: 8.50 cost units
Total Cost: 11.50 cost units
```

IMPORTANT: be careful with the string formatting in the `SecuritySuite` class; especially the new line character and the space after the `*` for every new component.

An example of what the return string format of the `total()` method when there are no protocols in the Security Suite is shown below:

```
Suite Components:
Total Cost: 0.00 cost units
```

Note: There is NO space after the colon on the first line, just a newline (i.e., `"Suite Components:\n"`). The `suite.total()` return value in the examples above do not contain a newline character (`\n`) at the end.

---

### Testing SecuritySuite

How to write a correct assert statement when a method's return value is a string that is very long and contains newlines?

You have two options (see the "miscellaneous" section in the [testing document](https://docs.google.com/document/d/e/2PACX-1vTbIEpAAAYTNv-zOMx5EP5bdbw-89na8jDUlQ45DBI8q8woNr41ho_DD6a9GPJlSB1SNUpjKrLlRTGK/pub). In your tests, you should create two security suites `suite1` and `suite2`, which are both tested in the TestSecuritySuite class's `test_total()` method.


## Testing your code

### testFile.py pytests

This file will contain unit tests using pytest to test if your functionality is correct. You should create your own tests different than the examples given in this writeup. Think of various scenarios and method calls to be certain that the state of your objects and return values are correct (provide enough tests such that all method calls in Protocol, Encryption, Authentication and SecuritySuite are covered). 

Even though Gradescope will not use this file when running the automated tests, it is important to provide this file with various test cases (testing is important!).
We will manually grade your `testFile.py` to make sure your unit tests cover the defined methods in Protocol, Encryption, Authentication and SecuritySuite.

## Submission

Once you're done with writing your class definition and tests, Submit your `Protocol.py`, `Encryption.py`, `Authentication.py`, `SecuritySuite.py`, and `testFile.py` files to the Lab02 assignment on Gradescope. There will be various unit tests Gradescope will run to ensure your code is working correctly based on the specifications given in this lab.

Note on grading for labs with testing component: For this lab assignment (and all lab assignments requiring a `testFile.py`), we will manually grade the tests you write. In general, your lab score will be based on the autograder's score (out of 100 points).

- If you write your tests correctly according to the specifications, then you will receive 100/100 points.
- If your written tests are missing, incomplete, or incorrect, then there will be up to a 10 point deduction from the autograder score. For example, if you didn't write any tests, then your lab score will be 90/100 (-10 point deduction from the autograder's score).
- Additionally, if the instructions are asking you to implement something in a certain way, e.g., to minimize code duplication, we might subtract points if your implementation does not follow these instructions.

---

# Troubleshooting


### "Autograder failed" error

```
The autograder failed to execute correctly...
```

Make sure your files don't have any print statements in them.  The classes should only be returning values, not printing.  testFile.py shouldn't have any output if all the tests pass; it should only produce an AssertionError when something's wrong with the code.

If you are testing your code with print statements, make sure to either add them inside the `if __name__ == "__main__":` block or comment them out before submitting your files to Gradescope.

---

```
ModuleNotFoundError: No module named ...
```
Check that you named your file EXACTLY as was specified - remember that Python is case-sensitive. Additionally, make sure that if you submitted the zip file, you didn't zip the folder: Gradescope expects just the files themselves.



---	

_Acknowledgment: This lab has been modified in collaboration with [Noah Spahn](https://github.com/noah-de) to incorporate cybersecurity context._
