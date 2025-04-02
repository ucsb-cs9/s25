# lab01 : Vulnerability Database - Python Classes

| num | ready? | description | assigned | due |
| ----- | ----- | ----- | ----- | ----- |
| [lab01](https://ucsb-cs9.github.io/s24-ykk/lab/lab01/) | true | Python Classes | Tue 04/09 11:00AM | Tue 04/16 11:59PM |

The second assignment is to create a vulnerability database. The practical skills to be developed include:

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