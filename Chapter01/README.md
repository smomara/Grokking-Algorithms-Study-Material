# Introduction to Algorithms

## Summary

Chapter 1 provides a foundation for the rest of the book by introducing the fundamental concepts of algorithms and their roles in problem-solving. 
It emphasizes the importance of selecting the right algorithm to optimize efficiency 
and introduces the concept of Big O notation as a tool for evaluating algorithm performance.

## Key Concepts

- Algorithms
- Efficiency and Optimization
- Big O Notation

## Code Snippets


### Binary Search
```python
def binary_search(list, item):
  low = 0
  high = len(list)-1
  
  while low <= high:
    mid = (low + high) / 2
    guess = list[mid]
    if guess == item:
      return mid
    if guess > item:
      high = mid - 1
    else:
      low = mid + 1
  return None

my_list = [1, 3, 5, 7, 9]

print(binary_serach(my_list, 3)) # => 1
print(binary_search(my_list, -1)) # => None
```

## Exercises

1. **Exercise 1.1**: 
Suppose you have a sorted list of 128 names, and you're searching through it using binary search. 
What's the maximum number of steps it would take?     
*Answer*: 7

2. **Exercise 1.2**: 
Suppose you double the size of the list. What's the maximum number of steps now?    
*Answer*: 8

3. **Exercise 1.3**: 
You have a name, and you want to find the person's phone number in the phone book. 
Give the runtime in Big O notation.    
*Answer*: O(log *n*)

4. **Exercise 1.4**: 
You want to read the numbers of every person in the phone book.
Give the runtime in Big O notation.    
*Answer*: O(*n*)

5. **Exercise 1.5**: 
You want to read the numbers of just the *A*s. 
Give the runtime in Big O notation.    
*Answer*: O(*n*). You may think, "I'm only doing this for 1 out of 26 characters, so the runtime should be O(*n*/26)." 
A simple rule to remember is, ignore numbers that are added, subtracted, multiplied, or divided. 
None of these are correct Big O run times: O(*n* + 26), O(*n* - 26), O(*n* * 26), O(n / 26). 
They're all the same as O(*n*)!

## Recap

- Binary search is a lot faster than simple search.
- O(log *n*) is faster than O(*n*), but it gets a lot faster once the list of items you're searching through grows.
- Algorithm speed isn't measured in seconds, but in terms of *growth* of an algorithm.
- Algorithm times are written in Big O notatoin.
