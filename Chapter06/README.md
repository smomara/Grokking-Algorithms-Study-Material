# Breadth-First Search

## Key Concepts

- Graphs
- Breadth-First Search
- Queues

## Summary

### Graphs
A graph models a set of connections. They are a way to model how different things are connected to one another. Graphs are made up of nodes (elements) and edges (what connects elements).

### Implementation of a Graph
A graph consists of several nodes that are connected to neighboring nodes. A hash table is used to express this relationship by mapping a node to all its neighbors.

Let's use this graph as an example:
```
joe ─────────── alice
├── bob           |
│   ├── andy      |
│   └── peggy ────┘
└── claire
    ├── tom
    └── johnny
```

Here's how the code would be written:
```python
graph = {} # initialize the graph
graph["joe"] = ["bob", "claire", "alice"] # joe points to bob, claire, and alice
grpah["bob"] = ["andy", "peggy"] # bob points to andy and peggy
graph["claire"] = ["tom", "johnny"] # claire points to tom and johnny
grpah["alice"] = ["peggy"] # alice points to peggy
graph["andy"] = [] # andy points to nobody
grpah["peggy"] = [] # peggy points to nobody
graph["tom"] = [] # tom points to nobody
graph["johnny"] = [] # johnny points to nobody
```

### Breadth-First Search
Breadth-first search is a search algorithm that runs on graphs and can help answer two types of questions:
1. Is there a path from node A to node B?
2. What is the shortes path from node A to node B?

In a breadth-first search, all the first degree nodes are searched, then the second degree nodes, and so on.

Think of it like this: you are looking for a mango seller among your friends. Your immediate friends are the first degree nodes, so you make a list of all your immediate friends and ask them. If none of them are mango sellers, you get a list of all your friends friends from them and ask all of them - those are the second degree nodes. If none of them are mango sellers, you will go to the next degree.

If no path is never found, then the path doesn't exist. If a path is found, since the nodes are searched degree by degree, the first path found is the shortest. That is how question 1 and 2 are answered.

See the code snippets for an implementation of a breadth-first search.

### Queues
A queue is a data structure that works exactly like a queue in real life. The first person to get in line is the first person to be taken out of line. 

Queues are similar to stacks in the sense that they only have two functions: enqueue and dequeue. Enqueue puts an elements at the back of the queue and dequeue removes the element at the front of the queue. 

A queue is called a FIFO data structure: First In, First Out. On the other hand, a stack called a LIFO data structure: Last In, First Out.

Since the first degree is searched first, the nodes will be queued in a FIFO manner with a queue.

## Code Snippets

### Implementing a Breadth-First Search
To implement the algorithm:
1. Keep a queue of items
3. Dequeue an item
4. Check if the item meets the condition
5. If it meets the condition, end the loop, if it doesn't add all connected nodes to the queue
6. Loop
7. If the queue is empty, no path is found and end the loop
You must also keep track of visited nodes so that an infinite loop does not occur.
```python
from collecitons import deque

# example graph
graph = {} # initialize the graph
graph["joe"] = ["bob", "claire", "alice"] # joe points to bob, claire, and alice
grpah["bob"] = ["andy", "peggy"] # bob points to andy and peggy
graph["claire"] = ["tom", "johnny"] # claire points to tom and johnny
grpah["alice"] = ["peggy"] # alice points to peggy
graph["andy"] = [] # andy points to nobody
grpah["peggy"] = [] # peggy points to nobody
graph["tom"] = [] # tom points to nobody
graph["johnny"] = [] # johnny points to nobody

def is_seller(name): # function to check if a person is a seller
  return name[-1] == "m" # for the sake of an example, let's say if the name ends with "m" then they're a seller

def bfs(name):
  queue = deque() # initialize the queue
  queue += graph["joe"]
  searched = set() # initialize a set to store searched nodes
  
  while queue: # while the queue is not empty
    person = queue.popleft() # dequeue an item
    if not person in searched: # if the person has not yet been searched
      if is_seller(person): # if they are a seller end the search, the shortest path has been found
        print(person + " is a seller!")
        return True
      else: # if they are not a seller, mark as visited and add all connected nodes to queue
        searched.add(person)
        queue += graph[person]
  return False

bfs_search("joe") # => tom is a seller!
```

## Exercises
For the next two exercises, run a breadth-first search and find the solution.
1. **Exercise 6.1**
Find the length of the shortest path from start to finish.
![image](https://github.com/smomara/Grokking-Algorithms-Study-Material/assets/33362830/417061be-5376-4c6e-99e6-895838d2f12c)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*Answer*: The shortest path has a length of 2.

3. **Exercise 6.2**: 
Find the length of the shortest path from "cab" to "bat".
![image](https://github.com/smomara/Grokking-Algorithms-Study-Material/assets/33362830/c7b078f1-5d79-4375-876d-630d439165ea)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*Answer*: The shortest path has a length of 2.

3. **Exercise 6.3**: 
Here's a small graph of my morning routine.
![image](https://github.com/smomara/Grokking-Algorithms-Study-Material/assets/33362830/3327ccac-0b0c-4677-a409-cf0e87328a8a)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;For these three lists, mark whether each one is valid or invalid
![image](https://github.com/smomara/Grokking-Algorithms-Study-Material/assets/33362830/86ab7250-9278-467c-b9d8-a22904296367)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*Answers*: A - Invalid; B - Valid; C - Invalid.

4. **Exercise 6.4**
Here's a larger graph. Make a valid list for this graph.
![image](https://github.com/smomara/Grokking-Algorithms-Study-Material/assets/33362830/93fcd85d-3bed-4c65-8dd7-00e5f22b26b3)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*Answer*: Wake up, exercise, shower, get dressed

5. **Exercise 6.5**
Which of the following graphs are also trees?
![image](https://github.com/smomara/Grokking-Algorithms-Study-Material/assets/33362830/61cef1cd-d913-4eae-9eb5-216b33f0d7ad)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*Answers*: A - Tree; B - Not a tree; C - Tree.

## Recap

- Breadth-first search tells you if there's a path from A to B.
- If there's a path, breadth-first search will find the shortest path.
- If you have a problem like "find the shortest X," try modeling your problem as a graph, and use breadth-first search to solve.
- A directed graph has arrows, and the relationship follows the direction of the arrow.
- Undirected graphs don't have arrows, and the relationship goes both ways.
- Queues are FIFO (First In, First Out).
- Stacks are LIFO (Last In, First Out).
- You need to check people in the order they were added to the search list, so the search list needs to be a queue. Otherwise, you won't get the shortest path.
- Once you check someone, make sure you don't check them again. Otherwise, you might end up in an infinite loop.
