---
num: "Lecture 1"
desc: "Introduction, Python Review"
ready: true
lecture_date: 2025-04-03 15:30:00.00-7:00
---

* [Slides folder]({{ site.slides_url }}){:target="_blank"}

---

### Code Clarity
- It is highly encouraged to use explicit parentheses to make your code clearer.
- Keep in mind that the `and` operator has higher precedence than some other logical operators in Python, such as `or`.

### Data Structures: Set vs. List
- **List (`list`)**: Ordered, allows duplicates, supports indexing.
- **Set (`set`)**: Unordered, no duplicates, supports set operations like union or intersection, just as in math.

```
# Sets vs lists

set1 = {1, 1, 1, 3}
list1 = [1, 1, 1, 3]

print(set1)
print(list1)
print(set(list1))
```

### Autograder
- Engaging with the lab material and calling our attention to improvements that could be made may result in extra credit at the end of the quarter.
- Think critically about the test cases you write to ensure your code is robust!
- If at least half of the students are affected by an issue, the instructor may consider making an accommodation.
- If your submission has a syntax error, the autograder will give a zero.
- Unlimited submissions are allowed on **Gradescope**

### Testing & Assertions
- It is impossible to prove a program is 100% correct.
- Labs require you to write additional `assert` statement to verify correctness.
- The autograder has more `assert` statements in the backend that will further validate your code.
- On the midterm and final, you will be required to write `assert` statements for a given function.


### Design activity

An example of how to store weaknesses and vulnerabilities with their related attributes:

```
# Using a list to keep track of the weakness and the related counts
# [200, 45, 1 , 3] 

# Alternatively, using a nested dictionary
threat_database = {
    "CWE-20": {
        "pillar": 200,
        "base": 45,
        "class": 1,
        "variant": 3
        },
    "CWE-200": {
        "pillar": None,
        "base": None,
        "class": None,
        "variant": None
        }
    }

# Two ways to retrieve values
print(threat_database["CWE-200"]["variant"])
print(threat_database.get("CWE-20").get("variant")) # less prone to errors

```

# iClicker notes

```
# The code from the iClicker question

cve_val = "CVE-2022-21668"
cwe_val = "CWE-400"
year = 2022

print(f'cve_val cwe_val year')
#print(f'{cve_val} '{cwe_val}' {(year)}' )

```

---
