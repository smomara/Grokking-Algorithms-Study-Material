# Greedy Algorithms

## Key Concepts

- NP-Complete Problems
- Approximation Algorithms
- Greedy Algorithms

## Summary

### The Classroom Scheduling Problem
With overlapping classroom run times, how does one maximise the amount of classes to be held?

The algorithm is very simple:
1. Pick the class that ends the soonest, this will be the first class
2. Now pick a class that starts after the first class and ends the soonest
3. Repeat step 2

In each step, you find the locally optimal solution and hope you're left with the globally optimal solution.

This greedy solution is the optimal solution.

### The Knapsack Problem
You are trying to maximize the value of the items you can place in a bag that only holds 35lbs.

The items are:
- A $3000 30lb Stereo
- A $2000 20lb Laptop
- A $1500 15lb Guitar

The greedy strategy is to take the most expensive item. But the most expensive item, the stereo, leaves room for nothing else.

This greedy solution gets us $3000, pretty close to the optimal solution of $3500.

Sometimes you need an algorithm that solves the problem just good enough, and thats where greedy solutions shine.

### The Set Covering Problem
You want to broadcast a radio show in the USA and reach listeners in all states. To minimize cost you want to minimize the number of stations you have to pay while maximizing the states they broadcast to.

Here's how you can find a solution:
1. List every possible subset of stations (aka the power set)
2. From these, pick the set with the smallest number of stations that covers all 50 states

However, this algorithm will take O(2^*n*) time, which isn't fast enough. There exists no algorithm that solves it fast enough. What do you do?

You approximate with an approximation algorithm. Here's a greedy algorithm that comes pretty close:
1. Pick the station that covers the most states that haven't been covered yet. It's OK if the station covers some states that haven't been covered already
2. Repeat until all the states are covered

Approximation algorithms like the one above are used when calculating the exact solution will take too much time. Greedy algorithms are great approximation solutions because they are simple. The algorithm above runs in O(*n*^2) time, much faster than the exact solution.

### NP-Complete Problems
An NP-complete problem is one where no efficient solution has been found. An example of an NP-complete problem is the traveling salesman problem.

When an NP-complete problem is encountered, the best approach is to approximate with a greedy algorithm.

In short:
- Greedy algorithms optimise locally, hopefully finding a global optimum
- NP complete problems have no known fast solutions
- Approximation algorithms including greedy algorithms are used to solve NP complete problems

## Code Snippets

### The Set Covering Problem
```python
states_needed = set(["mt", "wa", "or", "id", "nv", "ut", "ca", "az"])

stations = {}
stations[“kone”] = set([“id”, “nv”, “ut”])
stations[“ktwo”] = set([“wa”, “id”, “mt”])
stations[“kthree”] = set([“or”, “nv”, “ca”])
stations[“kfour”] = set([“nv”, “ut”])
stations[“kfive”] = set([“ca”, “az”])

final_stations = set()

while states_needed:
  best_station = None
  states_covered = set()
  
  for station, states_for_station in stations.items():
    covered = states_needed & states_for_station # & is a set intersection
    
    if len(covered) > len(states_covered):
      best_station = station
      states_covered = covered
      
    final_stations.add(best_station)
    states_needed -= states_covered

print(final_stations) # => {'kfive', 'kone', 'kthree', 'ktwo'}
```

## Exercises
1. **Exercise 8.1**
You work for a furniture company, and you have to ship furniture
 all over the country. You need to pack your truck with boxes. All
 the boxes are of different sizes, and you’re trying to maximize
 the space you use in each truck. How would you pick boxes to
 maximize space? Come up with a greedy strategy. Will that give
 you the optimal solution?    
*Answer*: A greedy strategy would be to pick the largest box that
 will fit in the remaining space, and repeat until you can’t pack any
more boxes. No, this won’t give you the optimal solution.

2. **Exercise 8.2**
You’re going to Europe, and you have seven days to see everything
 you can. You assign a point value to each item (how much you
 want to see it) and estimate how long it takes. How can you
 maximize the point total (seeing all the things you really want to
 see) during your stay? Come up with a greedy strategy. Will that
 give you the optimal solution?   
*Answer*: Keep picking the activity with the highest point value that you can still do in the time you have left. Stop when you can't do anything else. No, this won't give you the optimal solution.

For each of these algorithms, say whether its a greedy algorithm or not.

3. **Exercise 8.3**
Quicksort   
*Answer*: No.

4. **Exercise 8.4**
Breadth-first search   
*Answer*: Yes.

5. **Exercise 8.5**
Dijkstra's algorithm
*Answer*: Yes.

6. **Exercise 8.6**
A postman needs to deliver to 20 homes. He needs to find the shortes route that goes to all 20 homes. Is this an NP-complete problem?   
*Answer*: Yes.

7. **Exercise 8.7**
Finding the largest clique in a set of people. Is this an NP-complete problem?
*Answer*: Yes.

8. **Exercise 8.8**
You're making a map of the USA, and you need to color adjacent states with different colors. You have to find the minimum number of colors you need so that no two adjacent states are the same color. Is this an NP-complete problem?   
*Answer*: Yes.

## Recap

- Greedy algorithms optimize locally, hoping to end up with a global optimum.
- NP-complete problems have no known fast solution.
- If you have an NP-complete problem, your best bet is to use an approximatin problem.
- Greedy algorithms are easy to write and fast to run, so they make good approximation algorithms.
