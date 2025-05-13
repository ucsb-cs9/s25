---
num: "Lecture 10"
desc: "Linked Lists cont."
ready: false
lecture_date: 2025-05-08 15:30:00.00-7:00
---

* [Slides folder]({{ site.slides_url }}){:target="_blank"}

---

# Linked Lists

* Python lists are just one way to implement a List type structure
* The underlying structure of a Python List stores information in contiguous memory
	* This is why certain operations like inserting into index 0 requires the shifting of elements to make room
* There is another way to implement a List type structure that performs better in certain operations (and worse in others)
	* This way doesn’t organize data in contiguous memory, so maintaining the list structure doesn’t need to shift elements around
* **Linked Lists** are List collection structures that are not stored in contiguous memory
	* But this structure still provides relative positioning of the data in the List

## Node

* A `Node` is an item in the LinkedList
* A Node contains the data that we are storing in the list and a reference to the next Node in the Linked List

## LinkedList

* A `LinkedList` manages and maintains the chain of nodes as a List collection
* It contains a **head** reference to the **first** node in the Linked List chain
	* As long as we know where the first element is, we can walk down the Linked List and visit every node in the structure
* Methods in the LinkedList class should maintain the links between the nodes
	* These methods maintain the "links" between the nodes in order to keep the LinkedList structure in a valid state


Note that there are many variations on maintaining Linked Lists
	* Some variations improve the performance on certain methods
	* Examples:
		* Linked List with head AND tail references
		* Double-Linked List
		* Circular Linked List
		* etc.
	* Depending on what you need the data structure for, you can design variations to possibly improve your application



## LinkedList Implementation (based on Chapter 3.6.2)

See the slides for the visual explanation.

```
# LinkedList.py
class Node:
	def __init__(self, data):
		self.data = data
		self.next = None

	def get_data(self):
		return self.data

	def get_next(self):
		return self.next

	def set_data(self, newData):
		self.data = newData

	def set_next(self, newNext):
        self.next = newNext

class LinkedList:
	def __init__(self):
		self.head = None

	def is_empty(self):
		return self.head == None

	def prepend(self, item):
		temp = Node(item)
		temp.setNext(self.head)
		self.head = temp

	def size(self):
		temp = self.head
		count = 0
		while temp != None: 
			count += 1 # accumulator pattern
			temp = temp.get_next()
		return count

	def find(self, item):
		temp = self.head
		found = False # the book's way of returning the indicator
		while temp != None and not found:
			if temp.get_data() == item:
				found = True
			else:
				temp = temp.get_next()
		return found
```



* An Ordered Linked List is similar to an Unordered Linked List except the nodes in the list are ordered with respect to each other (e.g., sorted by some attribute)
* The implementation of both are similar, except we have to maintain the ordered property of the nodes when we manage the list
	* Most methods can be the same, but adding the node requires us to put a node in the correct position (instead of simply adding to the front of the list)
  * If we want to add an item, we have to be careful to keep the chain intact.
	* Consider two cases:
		1. Adding to the front of the Linked List
		2. Adding to the middle / end of the Linked List

![AddLinkedList.png](AddLinkedList.png)

<sub>(illustration courtesy Richert Wang))</sub>

* Let’s implement the `add` method to see what inserting an item in the middle of the list would look like
	* Note: at the moment, we will add this in the `LinkedList` class, but it would be better to implement this in an `OrderedLinkedList` class. We can do this because we'll only test the `add` method with sorted elements in the Linked List.

```
# add method to maintain an Ordered Linked List
def add(self, item):
	current = self.head
	previous = None
	stop = False

	# find the correct place in the list to add
	while current != None and not stop:
		if current.get_data() > item: # check the instructions for where == is supposed to be
			stop = True
		else:
			previous = current
			current = current.get_next()

	# create Node with item to add
	temp = Node(item)

	# Case 1: insert at the front of the list
	if previous == None:
		temp.set_next(self.head)
		self.head = temp
	else: # Case 2: insert not at front of list
		temp.set_next(current)
		previous.set_next(temp)
```


Similarly, we have two cases for when we are removing items:
```
	def remove(self, item):
		current = self.head
		
		if current == None: # empty list, nothing to do
			return

		previous = None
		found = False
		while not found: #Find the element
			if current == None:
				return
			if current.get_data() == item:
				found = True
			else:
				previous = current
				current = current.get_next()

		# Case 1: remove 1st element
		if found == True and previous == None: # previous tells us that we haven't moved yet
			self.head = current.get_next()
		
		# Case 2: remove not 1st element
		if found == True and previous != None:
			previous.set_next(current.get_next()) # effectively bypasses the current item, removing it
```

Note that the item and its data are still stored on disk, so that data will be available until it's overwritten by the system. A secure way to remove data would be to overwrite the values that are stored in `current` before updating the links.

### Testing the code

We need a way to get the list and to check that it stores what we expected.

```
# Method to get the items from front to back
def get_list_str(self):
	current = self.head
	output = ""
	while current != None:
		output += str(current.get_data()) + " "
		current = current.get_next()
	output = output[:len(output)-1] # remove end space (can also use .strip())
	return output
```

As mentioned earlier, we'll write the tests using our `LinkedList()` implementation.

```
# Test to check if adding elements maintain order
def test_insertIntoOrderedList():
	ll = LinkedList()
	ll.prepend(80)
	ll.prepend(70)
	ll.prepend(60)
	ll.add(65)
	assert ll.get_list_str() == "60 65 70 80"
	ll.add(5)
	assert ll.get_list_str() == "5 60 65 70 80"
	ll.add(90)
	assert ll.get_list_str() == "60 65 70 80 90"
```

---
