---
num: "Lecture 0"
desc: "Welcome and Python review"
ready: true
lecture_date: 2025-04-01 15:30:00.00-7:00
---

* [Slides folder]({{ site.slides_url }}){:target="_blank"}

---

# Code from class

Examples from the iClicker questions:

```
item = "Pizza"
price = 12

# PIZZA costs $12.00
print(f"{item.upper()} costs ${price:.5f}")
```

# Deconsructing dictionaries

Dictionaries allow us to implement the mapping from the key to the corresponding value. No duplicate keys: if we add the same key mapping to different values, each addtion of the same key overwrites the previous value with its new value (see 'Iowa' below). Keys have to be **immutable**, however, values can be of any data type.

```
capitals = { 'Iowa': 'DesMoines',
             'Iowa': ['Madison', 'DesMoines'],
             'Wisconsin': 'Madison'
}
```

---
