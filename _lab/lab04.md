
---
layout: lab
num: lab04
ready: false
desc: "Recursion 2"
assigned: 2024-04-01 11:00:00.00-7
due: 2024-04-08 23:59:59.59-7
---

# Lab04: Network Path Discovery using Stack-Based Traversal

## Learning Goals
In this lab, you'll practice:
- Utilizing a Stack to simulate network path discovery
- Understanding how traversal algorithms are applied in networking and cybersecurity
- Practice writing [pytests](https://docs.pytest.org/en/stable/) to ensure your solution is correct

Note: It is important that you start this lab early so you can utilize our office hours to seek assistance / ask clarifying questions during the week before the deadline if needed!

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
- Empty spaces (' ') represent accessible network nodes
- Walls ('+') represent inaccessible systems, firewalls, or offline nodes
- The goal ('G') represents the destination server or high-value target

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

The position `network[x][y]` represents a specific node in our network map.

## Traversing the Network
Your function will need to traverse the network given a starting coordinate.
As you traverse, you'll track the number of "hops" (steps) taken and replace the ' ' elements with the step number.
This simulates documenting the path of the penetration test.
You may traverse the network horizontally and vertically (not diagonally).
You must implement your traversal in following way:

 - When reaching a certain node, you must check and move counterclockwise in the following order: North, then West, then South, then East
 - You will always be given a starting coordinate. This will be the first step taken by the function.
 - You will traverse the network until you reach the target ('G'). Once you reach the target, your algorithm can stop.

Using the example network above with a starting position at `network[4][4]`, after your algorithm finishes, the network will have the following updates containing the number of hops:

```
['+', '+', '+', '+', 'G', '+'],
['+', 8, '+', 11, 12, '+'],
['+', 7, 9, 10, '+', '+'],
['+', 6, '+', '+', 2, '+'],
['+', 5, 4, 3, 1, '+'],
['+', '+', '+', '+', '+', '+']
```

## Utilizing a Stack for Network Path Discovery
In both network routing and security analysis, we need to systematically explore all possible paths while keeping track of previously visited nodes.
A Stack data structure is perfect for this "backtracking" approach, which is essential when dealing with complex networks with multiple potential paths.

As you traverse the network, you should:
1. Push visited node coordinates onto the Stack
2. Replace the empty space (' ') with the current hop number
3. Check adjacent nodes in the specified order
4. If no valid moves exist from current position, pop from the Stack and continue from the previous position

If the Stack becomes empty before reaching the destination, this means there is no accessible path to the target node - important information for both network administrators and security professionals!

## Instructions
For this lab, you will need to create three files:

1. Stack.py - file containing your class definition of a Python Stack using Python Lists
2. lab04.py - file containing your solution to writing the network_path_exists function (renamed from maze_path_exists)
3. testFile.py - file containing pytest functions testing if your solution works as expected

### lab04.py
This file will contain a single function definition `network_path_exists(network, start_x, start_y)`.
The network parameter will be the 2D List network as described above.
`start_x` and `start_y` are the starting coordinates used when traversing the network.
You may assume that the starting position is valid.
The `network_path_exists` function will utilize a Stack and update the network elements with the number of hops at each traversed position.
It should return `True` if a path exists and the target was reached, and return `False` if no path to the target exists.
### Stack.py
This file will contain a Stack class implementation exactly as the one covered in the book using Python Lists. This should contain a constructor (`__init__`), and the `isEmpty`, `push`, `pop`, `peek`, and `size` methods. Your solution must utilize the Stack data structure to manage the traversal through the network.
### testFile.py
This file will contain unit tests using pytest to test if your `network_path_exists` functionality is correct. You should create various network scenarios (with and without solutions) and check if the traversal is correct. Write at least one test where a solution exists (different than the one provided in these instructions), and another test where a solution does not exist.

## Cross-Disciplinary Relevance
Understanding traversal algorithms is essential in cybersecurity for:

1. **Networking**: Dynamically discovering routes when static routing tables fail and verifying connectivity between systems
2. **Cybersecurity**: Identifying potential attack paths through a network and testing network segmentation effectiveness
3. **Military Communications**: Establishing redundant communication paths in contested environments
4. **Graph Theory**: Solving reachability problems in directed graphs

By implementing this stack-based traversal algorithm, you're learning a fundamental approach used in network analysis tools, routing protocols, and security assessment frameworks that discover and analyze paths through networks.

## Submission
Once you're done with writing your class/function definitions and tests, submit your lab04.py, Stack.py and testFile.py files to the Lab04 assignment on Gradescope. There will be various unit tests Gradescope to ensure your code is working correctly based on the specifications given in this lab.
Remove any print statements in your submission as they may interfere with the autograder.

## Step-by-Step Network Traversal Process
To illustrate how our penetration testing algorithm works, let's walk through the following example:
Let's say the starting network map and stack looks like this: (first step already taken)
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
For each step, we check the 4 directions (north, west, south, east) one by one to see if there is an accessible node to explore.

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
    ['+', '+', '+', '+', 'G', '+']                  |   |
    ['+', ' ', '+', ' ', ' ', '+']                  |   |
    ['+', ' ', ' ', ' ', '+', '+']                  |   |
    ['+', ' ', '+', '+',  2 , '+']                  |   | <- pop
    ['+', ' ', ' ', ' ',  1 , '+'] <- back to node 1|4,4| <- backtrack position
    ['+', '+', '+', '+', '+', '+']                  |---|
]
```

## Troubleshooting Common Issues
When implementing your network penetration testing simulation, watch out for these common issues:

1. Initialization Error: Ensure that the starting coordinates (start_x, start_y) are used only once for initializing the starting position in the network. Incorrectly reusing or modifying these initial coordinates during the traversal can lead to inaccurate path tracking—similar to how misconfiguring your starting point in a security scan can invalidate your entire assessment.
2. Node Marking: Each node you explore must be immediately marked with the current hop number. This marking is crucial to avoid revisiting nodes and creating infinite loops—just as proper documentation during penetration testing helps avoid redundant work and ensures comprehensive coverage.
3. Stack Management: Properly manage the stack by ensuring that only viable paths are pushed onto it and that backtracking is handled correctly by popping the stack when no moves are possible. Poor stack management resembles inefficient penetration testing workflows where potential paths are either missed or redundantly explored.