# Dijkstra's Algorithm

## Key Concepts

- Weighted Graphs
- Dijkstra's Algorithm

## Summary

### Weighted Graphs
A weighted graph is a graph where each edge has a numerical value called a weight.

### Dijkstra's Algorithm
Breadth-first search finds the shortest route between two nodes. In contrast, Dijkstra's algorithm finds the smallest total weight between two nodes.

When a graph has weights, the shortest path might not be the most effective in terms of the weights, so Dijkstra's algorithm is used for weighted graphs.

These are the steps for Dijkstra's algorithm:
1. Find the node with the lowest weight
2. Check if there's a cheaper path to the neighbors of the cheapest node. If so, update their weights
3. Repeat for all nodes in the graph
4. Calculate the final path

Note that Dijkstra's algorithm only works with directed acyclic graphs.

Dijkstra's algorithm also only works with positive weights in the graph. If there are negative weights, use the [Bellman-Ford algorithm](https://www.youtube.com/watch?v=lyw4FaxrwHg)

### Implementing Dijkstra's Algorithm
This is the graph we will use for the example:
```
        6        2
start -----> A -----> finish
   \         ↑       ↗
  2 \        | 1    / 5
     \       |     /
      \ ---> B ---/  
```

To code this example, you'll need three hash tables:
```python
graph = {
  "start": {
    "A": 6,
    "B": 2
  },
  "A": {
    "finish": 1
  },
  "B": {
    "A": 3,
    "finish": 5
  },
  "finish": {}
}

costs = {
  "A": 6,
  "B": 2,
  "finish": float("infinity")
}

parents = {
  "A": "start",
  "B": "start",
  "finish": None
}
```
The costs and parents hash tables will be updated as the algorithm progresses.

The algorithm will follow these steps:
1. Grab the node with the lowest weight
2. Update the weight for its neighors
3. If any of the neighbors weights were updated, update their parent
4. Mark this node as processed
5. Repeat while there are nodes to process

Here is the code:
```python
def find_lowest_cost_node(costs):
  lowest_cost = float("inf")
  lowest_cost_node = None
  for node in costs: # go through each node
    cost = costs[node]
    if cost < lowest_cost and node not in processed: # if its the lowest cost so far and hasnt been processed yet
      lowest_cost = cost
      lowest_cost_node = node
  return lowest_cost_node

node = find_lowest_cost_node(costs) # find the lowest-cost node that hasn't been processed yet
while node is not None: # If all nodes have been processed, the loop is done
  cost = costs[node]
  neighbors = graph[node]
  for n in neighbors.keys(): # go through all neighbors of current node
    new_cost = cost + neighbors[n]
    if costs[n] > new_cost: # if its cheaper to get to this neighbor by going through the current node
      costs[n] = new_cost # update the cost for this neighbor
      parents[n] = node # and update the parent for this neighbor to the current node
  processed.append(node)
  node = find_lowest_cost_node(costs)
```

## Exercises
For the next two exercises, run a breadth-first search and find the solution.
1. **Exercise 7.1**
In each of these graphs, what is the weight of the shortest path from start to finish?

![image](https://github.com/smomara/Grokking-Algorithms-Study-Material/assets/33362830/f398069c-c5a0-43e1-b559-19e68f8991a5)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*Answers*: A - 8; B - 60; C - No shortest path possible because of a negative-weight cycle.

## Recap

- Breadth-first search is used to calculate the shortest path for an unweighted graph.
- Dijkstra's algorithm is used to calculate the shortest path for a weighted graph.
- Dijkstra's algorithm works when all the weights are positive and the graph is directed and acyclic.
- If you have negative weights, use the Bellman-Ford algorithm.
