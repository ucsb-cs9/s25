---
layout: lab
num: lab03
ready: true
desc: "Recursion"
assigned: 2025-04-22 11:00:00.00-7
due: 2025-04-29 23:59:59.59-7
---

# Learning Goals

In this lab, you’ll practice:

- Writing recursive functions based on a specification.
  - Define a base case (or cases)
  - Design the next smallest input that would trigger a recursive case
  - Determine the actions that need to happen in the recursive case as well as how to reduce the input to get it to trigger the base case
- Practice writing pytests to ensure your recursive functions are correct.

## Cybersecurity Context:

Recursion is frequently used in cybersecurity applications including password checking, directory traversal, network packet analysis, and cryptographic algorithms.
The recursive functions you'll implement in this lab represent simplified versions of real-world cybersecurity operations.

Before you get started, make sure to read up on recursion, specifically Chapter 4.2.

# Instructions

For this lab, you will need to create two files:

- `lab03.py` - file containing your solution to all recursive functions you will implement in this lab.
- `testFile.py` - file containing pytest functions testing all recursive functions you will implement in this lab.
  - Note: Gradescope’s autograder requires you to submit your `testFile.py` in order for it to run your code (hopefully you’re practicing TDD and use your tests to check correctness!). Gradescope will also require you to provide all function definitions (even if incorrect) in lab03.py in order to run the tests.

There will be no starter code for this assignment, but rather function descriptions are given in the specification below.

It’s recommended that you organize your lab work in its own directory. This way all files for a lab are located in a single folder. Also, this will be easy to import various files into your code using the import / from technique shown in lecture.

## Recursive function definitions and specifications

You will write five recursive functions for this lab. Each one is specified below. One example test will be given, but you should write 3 - 5 explicit tests for each function (think of edge cases and various interesting cases when writing your tests!).

Note: You must write each function recursively in order to receive any credit; you may receive a 0 for your implementation, even if Gradescope's tests pass. For this lab, you may not (and need not) define additional helper functions.

- `int_division(num, div)` - Simulate a simplified password strength calculation where num represents password complexity score and div represents a security threshold. The parameters num and div are positive integers (you may assume `num` is >= 0 and `div` is > 0). This recursive function recursively returns the quotient (i.e. num // div) without explicitly using the // or / operators, or a pre-defined function. In security terms, this represents how many security thresholds a password passes.

Hint: Think of how you would manually count how many security thresholds (div) your password complexity (num) passes. Each subtraction represents checking against one security criterion.

```
# Example test
assert int_division(27, 4) == 6  # Password with complexity 27 passes 6 security thresholds of value 4
```

- `count_vowels(text)` - This recursive function will take a string value (text) representing a network log entry and return the number of vowels (which for this exercise are 'A','E','I','O','U','a','e','i','o','u') that are found in it. In a simplified security model, this could represent identifying certain patterns in log files.

Hint: Start with the first character. If it's a vowel (representing a flagged pattern), count one; if not, don't. Either way, proceed to the rest of the string recursively.

```
# Example test
assert count_vowels("Access Denied From IP: 192.168.1.1") == 7  # 7 potential patterns detected
```

- `reverse_str(text)` - The parameter text is a string. This recursive function will return a string in the reverse order of text, simulating a very basic encoding technique sometimes used in simple security obfuscation. Note that the reverse of an empty string is an empty string.

Hint: In string encoding, the reverse of all but the first character, followed by the first character, results in the full string reversed. Use this pattern for your recursion.

```
# Example test
assert reverse_str("password123") == "321drowssap"  # Basic encoding of sensitive information
```

- `remove_seq(text, seq)` - The parameters text and seq are strings that contain at least one character. This recursive function will return a string where all occurrences of seq are removed in the order it appears in the string text, simulating detection and removal of suspicious patterns in data. Your solution SHOULD NOT use the string's replace(), index() or find() methods.

Hint: Compare the start of text to seq. If they match, remove seq from text (removing the malicious pattern) and continue recursively without the first part of text. If they don't match, keep the first character of text and continue to check the rest.

```
# Example test
assert remove_seq("code<script>malicious()</script>fragment", "<script>malicious()</script>") == "codefragment"
# The suspicious script tag pattern is identified and removed from the code
```

The fact that we are removing the occurences of the seq in the order they appear, means that in this function, we are not going back to recheck that we introduced a new seq in the earlier part of the string by removing its occurrence later. Here, we are assuming that the following function call remove_seq("ababcc", "abc") will return 'abc', not an empty string. (You can challenge yourself to see how your function needs to be modified to handle it recursively, but this is not part of this lab.)

Hints: Think of what your base case could be, test it - what's the simplest case where you don't need to do any work?

- Use sample short strings to figure out what the algorithm should be
- Try strings that contain and do not contain the sequence that needs to be replaced and see what actions need to take place in each case.
- Which one of these cases would trigger your base case?
  - text = 'abc', seq = 'b'
  - text = 'acb', seq = 'ab'
  - text = 'ab', seq = 'abc'

These recursive functions demonstrate fundamental concepts that appear in cybersecurity:

- Password strength calculations often involve checking against multiple criteria - recursively
- Port scanning tools recursively check network ports for vulnerabilities
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

Gradescope requires testFile.py to be submitted before running any autograded tests. You should write 3 - 5 tests per function.

The asserts will be marked 0 if some of the asserts in testFile.py fail.

Here's the structure for the test file that you can use to get started:

```
# testFile.py

def test_int_division():
    # from lab03 import int_division
    # uncomment the above import post completion of function in lab03.py
    # write your assert statements here
    pass # remove this after writing asserts

def test_count_vowels():
    # from lab03 import count_vowels
    # uncomment the above import post completion of function in lab03.py
    # write your assert statements here
    pass # remove this after writing asserts

def test_reverse_string():
    # from lab03 import reverse_str
    # uncomment the above import post completion of function in lab03.py
    # write your assert statements here
    pass # remove this after writing asserts

def test_remove_seq():
    # from lab03 import remove_seq
    # uncomment the above import post completion of function in lab03.py
    # write your assert statements here
    pass # remove this after writing asserts
```

_Acknowledgment: This lab has been modified in collaboration with [
(https://github.com/noah-de) to incorporate cybersecurity context._
