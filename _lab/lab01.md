# lab01 : Vulnerability Database - Python Classes

| num | ready? | description | assigned | due |
| ----- | ----- | ----- | ----- | ----- |
| [lab01](https://ucsb-cs9.github.io/s24-ykk/lab/lab01/) | true | Python Classes | Tue 04/09 11:00AM | Tue 04/16 11:59PM |

The second assignment is to create a vulnerability database to aid in keeping track of the vulnerabilities that you have been reading about and the weakness classes that they belong to.
Vulnerabilities are recorded in the authoritative list of [Common Vulnerabilities and Exposures (CVE)](https://www.cve.org/), and given a unique CVE identifier.
After analysis, each vulnerability is classified according to a known weakness that is among the [Common Weakness Enumeration (CWE)](https://cwe.mitre.org/) list.
These are important classifications (look up some of the examples in this lesson to learn more), but they are difficult for humans to process visually. 
Fortunately, you can make a data structure to help you keep track of this.

The practical skills to be developed include:

* Defining classes in Python  
* Defining methods in Python classes

Note: In general, it is always important to work on labs and reading early so you can gain the proper context and utilize our office hours to seek assistance / ask clarifying questions during the week before the deadline, if needed!

It is a good idea to read up on some tools we’ll use in this lab before you get started, specifically Chapter 1.4.2.1 (String Formatting) and 1.4.6 - 1.4.6.1 (Object Oriented Programming).

The main idea for this lab is to write a program that will organize Vulnerabilities into a Vulnerability list. The program should have the ability to add / remove / search for vulnerabilities.

# Instructions

We recommend that you organize your lab work for this lab in its own directory, e.g., lab01. This way all files for a lab are located in a single folder. Also, this will be easy to import various files into your code using the import \* from technique shown in lecture.

You will need to create three files (note that the file names are case-sensitive when we import them in Python!):

* `Vulnerability.py` - a file containing a class definition for a Vulnerability object.  
* `VulnDB.py` - a file containing a class definition for a VulnDB object.  
* `testFile.py` - a file with the tests for the class methods.

## `Vulnerability.py` class

The `Vulnerability.py` file will contain the definition of a Vulnerability record.

We will define the Vulnerability attributes as follows:

* **CVE** - str that represents the unique CVE identifier of the vulnerability. Your program should ensure this field will be stored as a Python alpha-numeric string, with the same format as is stored in MITRE (two dashes separating three sections of the identifier CVE-2025-31910).  
* **CWE** - str that represents the MITRE weakness classification of the vulnerability.
* **year** - int that represents the release year of a vulnerability.

You will write a constructor that allows the user to construct a Vulnerability object by passing in values for all of the fields. Your constructor should set these attributes with the value None by default.

* __init__(self, cve, cwe, year)

In addition to your constructor, your class definition should also support “setter” methods that can update the state of the Vulnerability objects:

Each Vulnerability object should be able to call a method `to_string()` that you will implement, which returns a str with all the vulnerability attributes EXACTLY as shown (i.e., the string should contain all attributes in the following EXACT format "CVE" (CWE) - YEAR):

```
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

IMPORTANT: The `.to_string()` return value in the example above does not contain a newline character (\n) at the end.

## `testFile.py`  - Test your code
To ensure that your methods return the correct values of correct types, create a file `testFile.py` to hold the tests for the methods.
Below are potential objects and corresponding assertions that you can include:
```
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

## `VulnDB.py`
The `VulnDB.py` file will contain the definition of a single VulnDB object.
An VulnDB object will contain a dictionary structure where the keys of the dictionary will be a str type representing a vulnerability weakness classification (all upper-case characters).
The dictionary value will be a list of Vulnerability objects that the VulnDB contains. Note that the order of the Vulnerabilities in the list is based on when the Vulnerability object was inserted into the dictionary structure (most recent Vulnerability inserted will be at the end of the list).

Your code should support the following constructor and methods:

- `__init__(self)` - Constructor that initializes the dictionary structure of the VulnDB class. Initially, this dictionary should be empty.
- `add_vuln(self, vuln)` - Adds a Vulnerability object (vuln) to the VulnDB. The inserted Vulnerability object should be added to the end of the list of existing vulnerabilities that are of the same cwe. You may assume that a vuln with the same attributes does not already exist in the VulnDB when this method is called.
- `does_vuln_exist(self, vuln)` - Returns a Boolean True if the parameter vuln (with matching cve, cwe, year) exists in the VulnDB. Returns False otherwise.
- `remove_vuln(self, vuln)` - Removes a Vulnerability object (vuln) from the VulnDB if it exists. Your code will need to check that the provided parameter vuln object has the same attributes (cve, cwe, year) as an existing vuln in the VulnDB, if it is to be removed from the VulnDB.
- `remove_cwe(self, cwe)` - Removes all vulnerabilities of a certain cwe from the VulnDB if it exists. Your code will need to remove the cwe entry from the VulnDB’s dictionary. Note: the provided cwe parameter value may be input in either lower / upper case.
- `get_vulnerabilities_by_cwe(self, cwe)` - Returns a string of all vulnerabilities of a certain cwe. This string should consist of a collection of strings - one line for each vuln.
  - Since each vuln will be in its own line within a single string, a newline character (\n) should be inserted between each line (if applicable) EXCEPT at the very last line where no newline character should exist.
  - The order of the Vulnerabilities in this string will be dictated by the order of the Vulnerabilities in the VulnDB’s list for the Vulnerabilities cwe.
  - The Vulnerability `toString()` method should be used when constructing this method’s return string.
  - If no Vulnerabilities of the specified cwe exist in the VulnDB, then this method returns an empty string ("").
  - Note: the cwe parameter value may be in either lower / upper case.

Given an example VulnDB, add the following objects and assertions to your `testFile.py`:

### remember to import the correct module into your `testFile.py`

```
vulnerabilities = VulnDB()
vuln1 = Vulnerability("CVE-2022-21668", "CWE-400", 2022)
vuln2 = Vulnerability()
vuln3 = Vulnerability("CVE-2020-7218", "CWE-400", 2020)
vulnerabilities.add_vuln(vuln1)
vulnerabilities.add_vuln(vuln2)
```

try to create more vuln objects and add them in the VulnDB, 
you must use assert statements as shown below to test if the vuln objects were inserted correctly to the VulnDB

```
assert vulnerabilities.does_vuln_exist(vuln1) == True
assert vulnerabilities.does_vuln_exist(vuln2) == True
assert vulnerabilities.does_vuln_exist(vuln3) == False

vulnerabilities.add_vuln(vuln3)
assert vulnerabilities.does_vuln_exist(vuln1) == True
assert vulnerabilities.does_vuln_exist(vuln2) == True
assert vulnerabilities.does_vuln_exist(vuln3) == True

vulnerabilities.remove_vuln(vuln1)
assert vulnerabilities.does_vuln_exist(vuln1) == False
assert vulnerabilities.does_vuln_exist(vuln2) == True
assert vulnerabilities.does_vuln_exist(vuln3) == True

```

do the same for the other vuln objects in the VulnDB. 
use the assert statements as shown to check if the vuln objects were removed correctly

```
vuln1 = Vulnerability("CVE-2022-21668", "CWE-400", 2022)
vuln2 = Vulnerability()
vuln3 = Vulnerability("CVE-2020-7218", "CWE-400", 2020)
vuln4 = Vulnerability("CVE-2022-21668", "CWE-1284", 2022)
vuln5 = Vulnerability("CVE-2008-1303", "CWE-20", 2008)

vulnerabilities = VulnDB()
vulnerabilities.add_vuln(vuln1)
vulnerabilities.add_vuln(vuln2)
vulnerabilities.add_vuln(vuln3)
vulnerabilities.add_vuln(vuln4)
vulnerabilities.add_vuln(vuln5)

assert vulnerabilities.get_vulnerabilities_by_cwe("CWE-400") == \
"CVE-2022-21668" (CWE-400) - 2022
"CVE-2020-7218" (CWE-400) - 2020)

assert vulnerabilities.get_vulnerabilities_by_cwe("CWE-1284") == \
CVE-2022-21668" (CWE-1284) - 2022
assert vulnerabilities.get_vulnerabilities_by_cwe("CWE-20") == ""
"CVE-2008-1303" (CWE-20) - 2008

# check that the removal is working correctly
vulnerabilities.remove_cwe("CWE-20")
assert vulnerabilities.get_vulnerabilities_by_cwe("CWE-400") == \
"CVE-2022-21668" (CWE-400) - 2022
"CVE-2020-7218" (CWE-400) - 2020)
assert vulnerabilities.get_vulnerabilities_by_cwe("CWE-1284") == \
CVE-2022-21668" (CWE-1284) - 2022
assert vulnerabilities.get_vulnerabilities_by_cwe("CWE-20") == ""

vulnerabilities.remove_cwe("CWE-1284") 
assert vulnerabilities.get_vulnerabilities_by_cwe("CWE-1284") == ""
assert vulnerabilities.get_vulnerabilities_by_cwe("CWE-400") == ""
assert vulnerabilities.get_vulnerabilities_by_cwe("CWE-20") == \
"CVE-2008-1303" (CWE-20) - 2008

vulnerabilities.remove_cwe("CWE-400")
assert vulnerabilities.get_vulnerabilities_by_cwe("CWE-1284") == ""
assert vulnerabilities.get_vulnerabilities_by_cwe("CWE-400") == ""
assert vulnerabilities.get_vulnerabilities_by_cwe("CWE-20") == ""
```

Please make sure that your logic for all the methods in `VulnDB.py` pass the above example assert statements. IMPORTANT: You are highly encouraged to test your code locally with additional assert statements before you submit your files to Gradescope - please do not use Gradescope to debug.

# Submission
Once you’re done with writing your class definition, submit your `testFile.py`, `Vulnerability.py`, and `VulnDB.py` to the Lab01 assignment on Gradescope. There will be various unit tests Gradescope will run to ensure your code is working correctly based on the specifications given in this lab.
If the tests don’t pass, you may get some error message that may or may not be obvious at this point. Don’t worry - if the tests didn’t pass, take a minute to think about what may have caused the error. Check the Troubleshooting guide below. If your tests didn’t pass and you’re still not sure why you’re getting the error, feel free to ask your TAs or Learning Assistants.

# Troubleshooting
```
ModuleNotFoundError: No module named ...
```
Check that you named your file EXACTLY as was specified - remember that Python is case-sensitive.

```
NoneType has no attribute ...
```
Remember that before you can use `.title()` or `.upper()` in your constructor, you need to verify that the parameter is a string instead of None. Use the if/else branches to differentiate between these cases.

_Acknowledgment: This lab has been modified in collaboration with [Noah Spahn](https://github.com/noah-de) to incorporate cybersecurity context._
