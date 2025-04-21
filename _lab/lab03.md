---
layout: lab
num: lab02
ready: true
desc: "Solving problems with Recursion"
assigned: ?
due: ?
---

# Learning Goals

In this lab, you’ll practice:

- Writing recursive functions based on a specification.
  - Define a base case (or cases)
  - Design the next smallest input that would trigger a recursive case
  - Determine the actions that need to happen in the recursive case as well as how to reduce the input to get it to trigger the base case
- Practice writing pytests to ensure your recursive functions are correct.

## Cybersecurity Context:

Recursion is frequently used in contexts where the problem is well defined and can be divided into smaller, similar subproblems.
The cybersecurity applications for recursion include security audits, password checking, directory traversal, network packet analysis, and cryptographic algorithms.
The recursive functions you'll implement in this lab represent simplified versions of real-world cybersecurity operations.

Before you get started, make sure to read up on recursion, specifically Chapter 4.2.

# Instructions

For this lab, you will need to create two files:

- `lab03.py` - file containing your solution to all recursive functions you will implement in this lab.
- `testFile.py` - file containing pytest functions testing all recursive functions you will implement in this lab.
  - Note: Gradescope’s autograder requires you to submit your `testFile.py` in order for it to run your code (hopefully you’re practicing TDD and use your tests to check correctness!). Gradescope will also require you to provide all function definitions (even if incorrect) in lab03.py in order to run the tests.

There will be no starter code for this assignment, but rather function descriptions are given in the specification below.

It’s recommended that you organize your lab work in its own directory.
This way all files for a lab are located in a single folder.
Also, this will be easy to import various files into your code using the import / from technique shown in lecture.

## Recursive function definitions and specifications

You will write two recursive functions for this lab. Each one is specified below.
One example test will be given, but you should write 3 - 5 explicit tests for each function (think of edge cases and various interesting cases when writing your tests!).

Note: You must write each function recursively in order to receive any credit; you may receive a 0 for your implementation, even if Gradescope's tests pass.
For this lab, you may not (and need not) define additional helper functions.

1. `find_insecure_configs(config_dict, parent_path="")` - The parameter is a json configuration file and optionally, a parent path.
This recursive function searches through nested data structures to find insecure configurations and returns a list of nested tuples with (path, value, reason) set for each insecure setting found.
The criteria to check for are:
    - `Security feature disabled`: Any boolean value False where the key contains "secure", "encrypt", or "auth"
    - `Development feature enabled`: Any boolean value True where the key contains "debug" or "test"
    - `Weak password policy`: Any password minimum length less than 8

    An example configuration is shown below:
    ```
    # Simple configuration example
    config = {
        "server": {
            "auth": {
                "require_ssl": False,  # Insecure: SSL disabled
                "min_password_length": 4  # Insecure: Weak password policy
            },
            "debug": True  # Insecure: Debug enabled
        },
        "database": {
            "encrypt_data": False,  # Insecure: Encryption disabled
            "connection": {
                "timeout": 30,  # Not insecure
                "retries": 3    # Not insecure
            }
        }
    }
    ```
    To test the recursive function, we could do the following:
    ```
    # Example test
    results = find_insecure_configs(config)
    assert(('server.debug', True, 'Development feature enabled') in results)
    ```

2. `analyze_packet_recursively(packet_data)` - The parameter text is a dictionary.
This function will check for five malicious patterns and return a list of suspicious elements found in the packet.

   There are five items to check for:
    1. Source IP addresses from suspicious ranges (e.g., 192.168.0.0/16 trying to access from outside)
    2. Unusual port combinations (e.g., connecting to port 3389 from outside)
    3. Fragmented IP packets (potential evasion technique)
    4. Suspicious HTTP paths (like containing "../" for path traversal or common attack patterns)
    5. Unusual user-agent strings

    Some examples of tests follow:

    ```
        # Example test
        def test_normal_packet():
            normal_packet = {
                "ethernet": {"src": "00:11:22:33:44:55", "dst": "66:77:88:99:aa:bb"},
                "ip": {"src": "10.0.0.1", "dst": "10.0.0.2"},
                "tcp": {"src_port": 12345, "dst_port": 80}
            }
        assert analyze_packet_recursively(normal_packet) == []

        def test_suspicious_packet():
            suspicious_packet = {
                "ip": {"src": "192.168.1.1", "dst": "8.8.8.8"},
                "tcp": {"src_port": 12345, "dst_port": 3389}
                }

            findings = analyze_packet_recursively(suspicious_packet)
            assert len(findings) == 2
            assert any("Private IP" in finding for finding in findings)
            assert any("sensitive port 3389" in finding for finding in findings)
    ```



3. `remove_seq(text, seq)` - The parameters text and seq are strings that contain at least one character. This recursive function will return a string where all occurrences of seq are removed in the order it appears in the string text, simulating detection and removal of suspicious patterns in data. Your solution SHOULD NOT use the string's replace(), index() or find() methods.

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

def find_insecure_configs(config_dict, parent_path=""):
    """
    Recursively searches through a nested dictionary (like JSON config)
    to find insecure configurations.

    Args:
        config_dict (dict): Dictionary representing configuration
        parent_path (str): Path in the config to current position (for recursive calls)

    Returns:
        list: List of tuples with (path, value) for insecure settings

    Example:
        >>> config = {
        ...     "server": {
        ...         "auth": {"require_ssl": False, "min_password_length": 4},
        ...         "debug": True
        ...     },
        ...     "database": {"encrypt": False}
        ... }
        >>> find_insecure_configs(config)
        [('server.auth.require_ssl', False), ('server.auth.min_password_length', 4),
         ('server.debug', True), ('database.encrypt', False)]
    """
    pass

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