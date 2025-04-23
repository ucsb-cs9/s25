---
layout: lab
num: lab03
ready: false
desc: "Functions calling themselves - Recursion"
assigned: 2025-04-23 11:00:00.00-7
due: 2025-04-29 23:59:59.59-7
---


# Learning Goals

In this lab, you’ll practice:

- Writing recursive functions based on a specification.
  - Define a base case (or cases)
  - Design the next smallest input that would trigger a recursive case
  - Determine the actions that need to happen in the recursive case as well as how to reduce the input to get it to trigger the base case
- Practice writing pytests to ensure your recursive functions are correct.


# Cybersecurity Context

Recursion is frequently used in cybersecurity applications including password checking, directory traversal, network packet analysis, and cryptographic algorithms.
The recursive functions you'll implement in this lab represent simplified versions of real-world cybersecurity operations to help you practice the structure and approach for creating recursive functions.

Before you get started, make sure to read up on recursion ([Chapter 5](https://runestone.academy/ns/books/published/pythonds/Recursion/toctree.html) of the electronic textbook).


# Instructions

For this lab, you will need to create two files:

- `lab03.py` - file containing your solution to all recursive functions you will implement in this lab.
- `testFile.py` - file containing pytest functions testing all recursive functions you will implement in this lab.
  - Note: Gradescope’s autograder requires you to submit your `testFile.py` in order for it to run your code (hopefully you’re practicing TDD and use your tests to check correctness!). Gradescope will also require you to provide **all** function definitions (even if incorrect) in lab03.py in order to run the tests.

---

## Recursive function definitions and specifications

For each recursive function, you need to write 3 - 5 explicit tests (think of bases cases, edge cases, and various interesting cases when writing your tests!).

Note: You must write each function **recursively** in order to receive any credit; you may receive a 0 for your implementation, even if Gradescope's tests pass. For this lab, you may not (and need not) define additional helper functions.

- `int_division(num, div)` - Simulate a simplified password strength calculation where `num` represents password complexity score and `div` represents a security threshold. The parameters `num` and `div` are positive integers (you may assume `num` is >= 0 and `div` is > 0). This recursive function recursively returns the quotient (i.e. `num // div`) without explicitly using the `//` or `/` operators, or a pre-defined function. In security terms, this represents the number of security thresholds a password passes.

Hint: Think of how you would manually count how many security thresholds (div) your password complexity (num) passes. Each subtraction represents checking against one security criterion.

```
# Example test
assert int_division(27, 4) == 6  # Password with complexity 27 passes 6 security thresholds of value 4
```

- `count_vowels(text)` - This recursive function will take a string value (text) representing a network log entry and return the number of vowels that are found in it. For this exercise, the vowels are `'A','E','I','O','U','a','e','I','o','u'`. In a simplified security model, this could represent identifying certain patterns in log files.

Hint: Start with the first character of the text. If it's a vowel (representing a flagged pattern), count one; if not, skip counting it. Either way, proceed to the rest of the string recursively (each time, looking at the first character).

```
# Example test
assert count_vowels("Access Denied From IP: 192.168.1.1") == 7  # 7 potential patterns detected
```

- `reverse_str(text)` - The parameter text is a string. This recursive function will return a string in the reverse order of text, simulating a very basic encoding technique sometimes used in simple security obfuscation. Note that the reverse of an empty string (`''`) is an empty string.

Hint: In string encoding, the reverse of all but the first character, followed by the first character, results in the full string reversed. Use this pattern for your recursion.

```
# Example test
assert reverse_str("password123") == "321drowssap"  # Basic encoding of sensitive information
```

- `remove_seq(text, seq)` - The parameters `text` and `seq` are strings that contain at least one character. This recursive function will return a string where all occurrences of `seq` are removed in the order it appears in the string text, simulating detection and removal of suspicious patterns in data. Your solution SHOULD NOT use the string's `.replace()`, `.index()` or `.find()` methods.

Hint: Compare the start of `text` to `seq` (think of string slicing). If they match, remove `seq` from text (removing the malicious pattern) and continue recursively without the first part of text that you already checked. If they don't match, keep the first character of text and continue to check the rest.

```
# Example test
assert remove_seq("code<script>malicious()</script>fragment", "<script>malicious()</script>") == "codefragment"
# The suspicious script tag pattern is identified and removed from the code
```

The fact that we are removing the occurrences of the `seq` in the order they appear, means that in this function, we are not going back to recheck that we introduced a new `seq` in the earlier part of the string by removing its occurrence later. Here, we are assuming that the following function call `remove_seq("ababcc", "abc")` will return `'abc'`, _not_ an empty string. (You can challenge yourself to see how your function needs to be modified to handle it recursively, but this is not part of this lab.)

Hints: Think of what your base case could be, test it - what's the simplest case where you don't need to do any work?

- Use sample short strings to figure out what the algorithm should be
- Try strings that contain and do not contain the sequence that needs to be replaced and see what actions need to take place in each case.
- Which one of these cases would trigger your base case?
  - text = 'abc', seq = 'b'
  - text = 'acb', seq = 'ab'
  - text = 'ab', seq = 'abc'


- `locate_files(dir)` - The parameter `dir` is a dictionary that contains keys that map to either `None` OR dicts. If the key maps to `None`, then this key is a filename, otherwise, it is a dictionary that needs to be traversed to extract its contents. The recursive function will return a list of the **full paths** of each of the files.

For example, given the following dictionary, lab00, lab01, and tests are folders (directories) because their corresponding value is a dictionary, whereas the other keys have `None` as their corresponding value, indicating that those keys are filenames. Hence, the path to the `README.md` consists of the keys that lead to it, separated by slashes `/`, i.e., `"lab00/README.md"`:
```
files = {
    "lab00" : {
        "tests" : {
            "test.py" : None
            },
        "lab00.py" : None,
        "README.md" : None
        },
    "lab01" : {
        "params.txt" : None,
        "lab01.py" : None
        },
    "base.py" : None
    }
```

Test your function, making sure that it is returning a list. If the dictionary is empty, the function should return an empty list.

```
# Example test
files = {"lab00" : {"tests" : {"test.py" : None}, "lab00.py" : None, "README.md" : None}, "lab01" : {"params.txt" : None, "lab01.py" : None}, "base.py" : None }
assert locate_files(files) == ["lab00/test/test.py", "lab00/lab00.py", "lab00/README.md", "lab01/params.txt", "lab01/lab01.py", "base.py"]
# The files are labelled and put into a list for easy scanning
```

Use the following code framework to begin with:
```
def locate_files(dir):
  all_files = []
  for key in dir.keys():
    # YOUR CODE HERE
    ...

    all_files.append(key + "/" + "__returned_value_from_recursive_call__") # TODO: change __returned_value_from_recursive_call__
  return all_files 
```

Hint: Your return type will always be the same, so how can you add the list that you returned from the recursion to `all_files`? Note, you will always need to include the directory that a file is in (its key) to the front of it before adding it to `all_files`.

---


These recursive functions demonstrate fundamental concepts that appear in cybersecurity:

- Password strength calculations often involve checking against multiple criteria - recursively
- Port and file scanning tools recursively check network ports/files for vulnerabilities or malware
- Pattern detection in log files and data streams often uses recursive parsing - techniques
- Simple encoding/obfuscation techniques like string reversal are basic security - measures
- Identifying and removing malicious patterns from code or data is essential in security operations

While these exercises are simplified versions, they introduce the recursive thinking patterns needed in cybersecurity applications.


## `testFile.py` pytest

This file will contain unit tests using pytest to test if your functionality is correct. Write your tests first in order to check the correctness of your recursive function. Consider including security-relevant test cases, such as:

- Testing password strength with common password patterns
- Testing port scanning with well-known service ports (22, 80, 443)
- Testing pattern detection with simulated security log entries
- Testing encoding/decoding with sensitive information patterns
- Testing pattern removal with common malicious script patterns

Gradescope requires `testFile.py` to be submitted before running any autograded tests. You should write 3 - 5 tests per function.

The asserts will be marked 0 if any of the asserts in `testFile.py` fail.

Here's the structure for the test file that you can use to get started:

```
# testFile.py

def test_int_division():
    # from lab03 import int_division
    # uncomment the above import after defining the function in lab03.py
    # write your assert statements here
    pass # remove this after writing asserts

def test_count_vowels():
    # from lab03 import count_vowels
    # uncomment the above import after defining the function in lab03.py
    # write your assert statements here
    pass # remove this after writing asserts

def test_reverse_string():
    # from lab03 import reverse_str
    # uncomment the above import after defining the function in lab03.py
    # write your assert statements here
    pass # remove this after writing asserts

def test_remove_seq():
    # from lab03 import remove_seq
    # uncomment the above import after defining the function in lab03.py
    # write your assert statements here
    pass # remove this after writing asserts

def test_locate_files():
    # from lab03 import locate_files
    # uncomment the above import after defining the function in lab03.py
    # write your assert statements here
    pass # remove this after writing asserts

```



---	

_Acknowledgment: This lab has been modified in collaboration with [Noah Spahn](https://github.com/noah-de) to incorporate cybersecurity context. Special thanks to CS9 S25 TAs Michelle Zimmermann and Hitomi Nakayama for incorporating a file location function._
