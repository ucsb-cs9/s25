# lab01 : Vulnerability Database - Python Classes

| num | ready? | description | assigned | due |
| ----- | ----- | ----- | ----- | ----- |
| [lab01](https://ucsb-cs9.github.io/s24-ykk/lab/lab01/) | true | Python Classes | Tue 04/09 11:00AM | Tue 04/16 11:59PM |

The second assignment is to create a vulnerability database to aid in keeping track of the vulnerabilities that you have been reading about and the weakness classes that they belong to.
Vulnerabilities are recorded in the authoritative list of [Common Vulnerabilities and Exposures (CVE)](https://www.cve.org/), and given a unique CVE identifier.
After analysis, each vulnerability is classified according to a known weakness that is among the [Common Weakness Enumeration (CWE)](https://cwe.mitre.org/) list.

The practical skills to be developed include:

* Defining classes in Python  
* Defining methods in Python classes

Note: In general, it is always important to work on labs and reading early so you can gain the proper context and utilize our office hours to seek assistance / ask clarifying questions during the week before the deadline, if needed\!

It is a good idea to read up on some tools we’ll use in this lab before you get started, specifically Chapter 1.4.2.1 (String Formatting) and 1.4.6 \- 1.4.6.1 (Object Oriented Programming).

The main idea for this lab is to write a program that will organize Movies into a Movie list. The program should have the ability to add / remove / search for movies.

# Instructions

We recommend that you organize your lab work for this lab in its own directory, e.g., lab01. This way all files for a lab are located in a single folder. Also, this will be easy to import various files into your code using the import \* from technique shown in lecture.

You will need to create three files (note that the file names are case-sensitive when we import them in Python\!):

* Vulnerability.py \- a file containing a class definition for a Vulnerability object.  
* VulnDB.py \- a file containing a class definition for a VulnDB object.  
* testFile.py \- a file with the tests for the class methods.

## Vulnerability.py class

The Vulnerability.py file will contain the definition of a Vulnerability record.

We will define the Vulnerability attributes as follows:

* **CVE** \- str that represents the unique CVE identifier of the vulnerability. Your program should ensure this field will be stored as a Python alpha-numeric string, with the same format as is stored in MITRE (two dashes separating three sections of the identifier CVE-2025-31910).  
* **CWE** \- str that represents the MITRE weakness classification of the vulnerability. Your program should ensure that this field will be stored in [Title case](https://docs.python.org/3/library/stdtypes.html#str.title).  
* **year** \- int that represents the release year of a vulnerability.

You will write a constructor that allows the user to construct a Movie object by passing in values for all of the fields. Your constructor should set these attributes with the value None by default.

* \_\_init\_\_(self, cve, cwe, year)

In addition to your constructor, your class definition should also support “setter” methods that can update the state of the Vulnerability objects:

Each Vulnerability object should be able to call a method to_string() that you will implement, which returns a str with all the vulnerability attributes EXACTLY as shown (i.e., the string should contain all attributes in the following EXACT format "CVE" (CWE) - YEAR):

```python
vulnerability1 = Vulnerability("CVE-2024-37032", "CWE-20", 2024)
print(vulnerability1.to_string())
print() # separate two vulnerabilities with a newline
vulnerability2 = Vulnerability("CVE-2024-3402", "CWE-1426", 2024)
print(vulnerability2.to_string())
```

Output:
```
"CVE-2024-37032" (CWE-20) - 2024
"CVE-2024-3402" (CWE-1426) - 2024
```

IMPORTANT: The .to_string() return value in the example above does not contain a newline character (\n) at the end.

## Test your code
To ensure that your methods return the correct values of correct types, create a file testFile.py to hold the tests for the methods.
Below are potential objects and corresponding assertions that you can include:
```Python
from Vulnerability import Vulnerability

vuln0 = Vulnerability()
assert vuln0.cve == None
### TODO: write additional asserts for the other methods
### to test the default form of the constructor

vuln1 = Vulnerability("CVE-2008-1303", "CWE-20", 2008)
assert vuln1.cve == "CVE-2008-1303"
### TODO: write additional asserts for the other methods
assert vuln1.to_string() == '"CVE-2008-1303" (CWE-20) - 2008'

### TODO: write additional asserts for at least one other vulnerability
```
