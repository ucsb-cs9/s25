---
layout: lab
num: lab04
ready: true
desc: "Network Path Discovery using Stacks"
assigned: 2025-04-29 11:00:00.00-7
due: 2024-05-08 23:59:59.59-7
---

# Lab04: Network Path Discovery using Stack-Based Traversal

## Learning Goals
In this lab, you'll practice:
- Utilizing a Stack to simulate network path discovery
- Understanding how traversal algorithms are applied in networking and cybersecurity
- Practice writing [pytests](https://docs.pytest.org/en/stable/) to ensure your solution is correct

Note: It is important that you start this lab early so you can utilize our office hours to seek assistance / ask clarifying questions during the week before the deadline if needed!

More context on this specific problem is covered in the book (See **Recursion Chapter 4.6: Exploring a Maze**, or [5.11 in the online book](https://runestone.academy/ns/books/published/pythonds/Recursion/ExploringaMaze.html)). The book explains how this problem can be solved recursively, but in this lab we will **_not_ use recursion** - rather we will do what recursion does for us and **manually** keep track of positions visited using our implementation of a Stack data structure.


If you'd like an additional walkthrough, here's a 15-minute handwritten video explanation of how to approach solving a maze using the logic from this lab:
<https://www.loom.com/share/b3323f2125d447dcbc7d18b96e45dda4?sid=092fe2c5-cf90-48fa-ae40-ead8c12c86c7>



## Network Path Discovery: Multiple Real-World Applications

### Traditional Networking Context
In computer networks, routers need to find paths from source to destination while navigating around offline nodes, congested links, or other obstacles. When traditional routing tables fail or need to be rebuilt, algorithms must discover alternate paths to maintain connectivity.

Network engineers also need tools to verify network connectivity - confirming whether a path exists between two points in the network and identifying the specific route packets would take. This is essential for both designing networks and troubleshooting connectivity issues.

### Cybersecurity Context
This same path-finding problem appears in cybersecurity contexts:

- Military operations may need to identify alternative communication routes when primary channels are compromised
- Cybersecurity penetration testers (ethical hackers hired to test security) need to discover possible paths through a network to reach sensitive assets
- Security analysts trace potential attack paths through network infrastructure to identify vulnerabilities before malicious actors can exploit them

Both scenarios involve a problem that can be modeled similarly to solving a maze, where:
- Empty spaces (`' '`) represent accessible network nodes
- Walls (`'+'`) represent inaccessible systems, firewalls, or offline nodes
- The goal (`'G'`) represents the destination server or high-value target

Your task is to implement a "network path discovery simulator" that determines if there's a path from a starting node to a destination, while documenting the hop count along the traversal path.

## Representing a Network
We'll represent a network as an `n x m` 2D List, similar to how we would represent a maze:

```
network = [
    ['+','+','+','+','G','+'],
    ['+',' ','+',' ',' ','+'],
    ['+',' ',' ',' ','+','+'],
    ['+',' ','+','+',' ','+'],
    ['+',' ',' ',' ',' ','+'],
    ['+','+','+','+','+','+'] ]
```

In this representation:

- `' '` - An active network node that can relay packets
- `'+'` - An offline node or blocked connection
- `'G'` - The destination node we're trying to reach

In the above example,
- `network[0]` contains a list, which represents the top row of the network map (containing the destination (`'G'`))
- Since we're dealing with Python 2D Lists (a Python list where the elements are Python Lists), the indices of the coordinates start with 0.
- You may assume that a network map will always be enclosed with a border (`'+'`) or the Goal (`'G'`) - there won't be any open spaces along the borders.

The position `network[x][y]` represents a specific node in our network map. 
- `network[0][0]` represents top left corner of the network
- `network[0][5]` represents top right corner of the network
- `network[0][4]` represents the location of the `'G'` node


**Note: This layout is different than a traditional cartesian coordinate system. As we move right the _y_ value increases, as we move left the _y_ value decreases, as we move up the _x_ value decreases, and as we move down the _x_ value increases.**


If we do reach a part of the network from which we cannot move anywhere, a Stack data structure can help us keep track of coordinates we've visited and allow us to "backtrack" to a certain point.



## Traversing the Network
- Your function will need to traverse the network given a starting coordinate.
- As you traverse, you'll track the number of "hops" (steps) taken and replace the blank `' '` elements with the step number.
    - This simulates documenting the path of the penetration test.
- You may traverse the network horizontally and vertically (not diagonally).

You must implement your traversal in following way:
 - When reaching a certain node, you must check and move **counterclockwise** in the following order: **North, then West, then South, then East**
 - You will always be given a starting coordinate. This will be the first step taken by the function (marked with a `1`).
 - You will traverse the network until you reach the target (`'G'`). Once you reach the target, your algorithm should stop (no need to keep traversing the network)
	* **Note: in the edge case where the current position is next to the goal, your function should always attempt to move into the space _before_ it checks to see if the position stepped into is the goal.**

By following these numbered steps, you can trace how the algorithm was traversing the 2D lists to reach the goal.

**Note that `'G'` or `'+'` should never be overwritten during the traversal.**

Remember: Lists (and 2D Lists) are mutable, so we should be able to change the network structure as our algorithm progresses and it should keep these changes! 


Using the example network above with a starting position at `network[4][4]`, after your algorithm finishes, the network will have the following updates containing the number of hops (see the explanation of the steps below):

```
['+', '+', '+', '+', 'G', '+'],
['+', 8, '+', 11, 12, '+'],
['+', 7, 9, 10, '+', '+'],
['+', 6, '+', '+', 2, '+'],
['+', 5, 4, 3, 1, '+'],
['+', '+', '+', '+', '+', '+']
```


This format is great for writing the assertion but
not too easy on the eyes, so we're providing a helper function below that you can use.

Please use it to debug your code and print out the state of the network in a more user-friendly way:

```
def print_nodes(network):
	for row in range(len(network)):
		for col in range(len(network[0])):
			print(f"|{network[row][col]:<2}", sep='',end='')
		print("|")
```

**Copy this function into your lab file and use it during the development and testing of the algorithm.** Once you are done testing your code, comment-out or remove the printing.

When we print the initial network, we should get the following format:

```
|+ |+ |+ |+ |G |+ |
|+ |  |+ |  |  |+ |
|+ |  |  |  |+ |+ |
|+ |  |+ |+ |  |+ |
|+ |  |  |  |  |+ |
|+ |+ |+ |+ |+ |+ |
```

After our algorithm runs, we should get the following format:

```
|+ |+ |+ |+ |G |+ |
|+ |8 |+ |11|12|+ |
|+ |7 |9 |10|+ |+ |
|+ |6 |+ |+ |2 |+ |
|+ |5 |4 |3 |1 |+ |
|+ |+ |+ |+ |+ |+ |
```

**Explanation of the steps**: 
-  Note that our starting coordinate (`network[4][4]`) is the first step we take (and mark the grid with a 1). 
- The algorithm then traverses North (step 2), at which point it can't go any further.
  - For example, in step 2's position (at coordinate `network[3][4]`), it tries to check North (runs into a wall), then West (runs into a wall), then South (already visited), then East (runs into a wall), so it can't continue.
  - At this point, the code needs to "backtrack" to step 1 and check the other counterclockwise directions of `network[4][4]`.
- Going back to step 1 (by popping step 2 coordinates off the stack), it tries to go North (already visited as indicated with step 2), then West, which is open (can continue, so now it takes the 3rd step), and so on. 

Additional instructions and the visualization of the stack are shown in the **Step-by-Step Network Traversal Process** below (and in the video linked above).


## Utilizing a Stack for Network Path Discovery
In both network routing and security analysis, we need to systematically explore all possible paths while keeping track of previously visited nodes.
A Stack data structure is perfect for this "backtracking" approach, which is essential when dealing with complex networks with multiple potential paths.

As you traverse the network, you should:
1. Push visited node coordinates onto the Stack
2. Replace the empty space (`' '`) with the current hop number
3. Check adjacent nodes in the specified order
4. If no valid moves exist from current position, pop from the Stack and continue from the previous position

If the Stack becomes empty before reaching the destination, this means there is no accessible path to the target node - important information for both network administrators and security professionals!

## Instructions
For this lab, you will need to create three files:

1. **Stack.py** - file containing your class definition of a Python Stack using Python Lists
2. **lab04.py** - file containing your solution to writing the `network_path_exists()` function as described in this writeup
3. **testFile.py** - file containing pytest functions testing if your solution works as expected


### lab04.py
This file will contain a single function definition `network_path_exists(network, start_x, start_y)`.
- The `network` parameter will be the 2D List network as described above.
- `start_x` and `start_y` are the starting coordinates used when traversing the network.
- You may assume that the starting position is valid.

The `network_path_exists()` function will utilize a Stack and update the network elements with the number of hops at each traversed position.
It should return `True` if a path exists and the target was reached, and return `False` if no path to the target exists.

### Stack.py
This file will contain a `Stack` class implementation exactly as the one covered in the book using Python Lists. This should contain a constructor (`__init__`), and the `isEmpty`, `push`, `pop`, `peek`, and `size` methods. Your solution **must** utilize this Stack data structure to manage the traversal through the network.

### testFile.py
This file will contain unit tests using pytest to test if your `network_path_exists()` functionality is correct. You should create various network scenarios (with and without solutions) and check if the traversal is correct. Write at least one test where a solution exists (different than the one provided in these instructions), and another test where a solution does not exist.

Remember that testing can help you debug your algorithm and ensure your functionality works as expected. First, check the return value of the function, then verify that the network after the function execution looks as expected. Solving the path through the network on paper can help you write these test cases.

Start with a simple case first and then place the goal in each direction to verify that the traversal happens correctly. For example, given the network configuration below, try the starting point at `(1, 1)` and `(4, 1)` to check that your function can correctly move in a single path. 

```
network_6x3 = [
    ['+','+','+'],
    ['+',' ','+'],
    ['+','G','+'],
    ['+',' ','+'],
    ['+',' ','+'],
    ['+','+','+'] ]
```

Then, add another network configuration and check the horizontal directions. Once you are confident that your code works for those cases, begin checking the cases with turns.


## Cross-Disciplinary Relevance
Understanding traversal algorithms is essential in cybersecurity for:

1. **Networking**: Dynamically discovering routes when static routing tables fail and verifying connectivity between systems
2. **Cybersecurity**: Identifying potential attack paths through a network and testing network segmentation effectiveness
3. **Military Communications**: Establishing redundant communication paths in contested environments
4. **Graph Theory**: Solving reachability problems in directed graphs

By implementing this stack-based traversal algorithm, you're learning a fundamental approach used in network analysis tools, routing protocols, and security assessment frameworks that discover and analyze paths through networks.

## Submission
Once you're done with writing your class/function definitions and tests, submit your files to the Lab04 assignment on Gradescope. There will be various unit tests Gradescope to ensure your code is working correctly based on the specifications given in this lab.

emove any print statements in your submission as they may interfere with the autograder.


---

## Step-by-Step Network Traversal Process
To illustrate how our penetration testing algorithm works, let's walk through the following example.

Let's say the starting network map and the stack looks like this: (first step already taken)
```
[
    ['+', '+', '+', '+', 'G', '+']                  |   |
    ['+', ' ', '+', ' ', ' ', '+']                  |   |
    ['+', ' ', ' ', ' ', '+', '+']                  |   |
    ['+', ' ', '+', '+', ' ', '+']                  |   |
    ['+', ' ', ' ', ' ',  1 , '+'] <- current node  |4,4| <- node coordinates in stack
    ['+', '+', '+', '+', '+', '+']                  |---|
]
```

For each step, we check the 4 directions (north, west, south, east) one by one to find the first accessible node to explore.
```
[
    ['+', '+', '+', '+', 'G', '+']                  |   |
    ['+', ' ', '+', ' ', ' ', '+']                  |   |
    ['+', ' ', ' ', ' ', '+', '+']                  |   |
    ['+', ' ', '+', '+',    , '+'] <- north is open |   |
    ['+', ' ', ' ', ' ',  1 , '+']                  |4,4|
    ['+', '+', '+', '+', '+', '+']                  |---|
]
```

Since the northern node is accessible, we move to that node and update the network map and the stack accordingly:
```
[
    ['+', '+', '+', '+', 'G', '+']                  |   |
    ['+', ' ', '+', ' ', ' ', '+']                  |   |
    ['+', ' ', ' ', ' ', '+', '+']                  |   |
    ['+', ' ', '+', '+',  2 , '+'] <- current node  |3,4| <- new position in stack
    ['+', ' ', ' ', ' ',  1 , '+']                  |4,4|
    ['+', '+', '+', '+', '+', '+']                  |---|
]
```

Now, from node 2, we check the 4 directions (North, West, South, East) one by one to see if there is an accessible node.
```
[
    ['+', '+', '+', '+', 'G', '+']                  |   |
    ['+', ' ', '+', ' ', ' ', '+']                  |   |
    ['+', ' ', ' ', ' ', '+', '+']                  |   |
    ['+', ' ', '+', '+',  2 , '+'] <- all blocked   |3,4|
    ['+', ' ', ' ', ' ',  1 , '+']                  |4,4|
    ['+', '+', '+', '+', '+', '+']                  |---|
]
```

When all 4 directions are blocked (N: firewall, W: firewall, S: already visited, E: firewall), we need to backtrack by popping the stack:
```
[
    ['+', '+', '+', '+', 'G', '+']                     |   |
    ['+', ' ', '+', ' ', ' ', '+']                     |   |
    ['+', ' ', ' ', ' ', '+', '+']                     |   |
    ['+', ' ', '+', '+',  2 , '+']                     |   | <- pop
    ['+', ' ', ' ', ' ',  1 , '+'] <- back to node 1   |4,4| <- backtrack position
    ['+', '+', '+', '+', '+', '+']                     |---|
]
```

You can go back up to the lab instructions and re-read the **Explanation of the steps** section to see how the algorithm can take the ext step after backtracking.

Starting from 1, again, the north has been visited, and since the west is open, we go west:

```
[
	['+', '+', '+', '+', 'G', '+']                  |   |
	['+', ' ', '+', ' ', ' ', '+']                  |   |
	['+', ' ', ' ', ' ', '+', '+']                  |   |
	['+', ' ', '+', '+',  2 , '+']                  |4,3| <- keep track of where we are
	['+', ' ', ' ',  3 ,  1 , '+'] <- now at 3      |4,4|
	['+', '+', '+', '+', '+', '+']                  |---|
]
```

---

## Troubleshooting Common Issues
When implementing your network penetration testing simulation, watch out for these common issues:

1) `The autograder failed to execute correctly. Please ensure that your submission is valid. ...` Remove the `print()` statements from your code or place them inside the `if __name__ == "__main__":` block to not interfere with the autograder tests. You want to make sure that the final product that you are delivering does not have any debugging statements when someone is importing your code for testing.

   
2) Initialization Error: Ensure that the starting coordinates `(start_x, start_y)` are used only **once** for initializing the starting position in the network. Incorrectly reusing or modifying these initial coordinates during the traversal can lead to inaccurate path tracking. This issue is similar to how misconfiguring your starting point in a security scan can invalidate your entire assessment.

   
3) Node Marking: Each node you explore must be immediately marked with the current hop number. This marking is crucial to avoid revisiting nodes and creating infinite loops; just as proper documentation during penetration testing helps avoid redundant work and ensures comprehensive coverage.


4) Stack Management: Properly manage the stack by ensuring that only viable paths are pushed onto it and that backtracking is handled correctly by popping the stack when no moves are possible. Poor stack management resembles inefficient penetration testing workflows where potential paths are either missed or redundantly explored.

5) If you run the pytest and all you see is "`collected N items`" without the actual results of those `N` tests, then it means that you have an infinite loop in one of your tests. You need to press `Ctrl + C` to stop it and see that the tests didn't finish running.

```
python3 -m pytest testFile.py
======================= test session starts =======================
platform darwin -- Python 3.13.1, pytest-8.3.5, pluggy-1.5.0
rootdir: /.../...
collected 3 items

testFile.py                 
^C

!!!!!!!!!!!!!!!!!!!!!!!! KeyboardInterrupt !!!!!!!!!!!!!!!!!!!!!!!!
/Users/sunrise/Documents/cs9-s25/lab04/332265328/Stack.py:6: KeyboardInterrupt
(to show a full traceback on KeyboardInterrupt use --full-trace)
===================== no tests ran in 18.89s =====================
```

**Debugging Recommendation**: Test each test, one at a time (you can just comment-out all other tests). Add the `print_nodes()` function call to your `network_path_exists()` function to check the state of the network on each iteration and to see where the updating of the grid is breaking down.


---

_Acknowledgment: Original lab specifications are courtesy Richert Wang. This lab has been modified in collaboration with [Noah Spahn](https://github.com/noah-de) to incorporate cybersecurity context._
