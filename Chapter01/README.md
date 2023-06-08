# Introduction to Algorithms

## Key Concepts

- Algorithms
- Binary Search
- Efficiency and Optimization
- Big O Notation

## Summary

### Introduction
An algorithm is a set of instructions for accomplishing a task

### Binary Search
Binary search is an algorithm used to search for a specific target value within a *sorted* array. The algorithm works by repeatedly dividing the space in half, narrowing down the possible range of values until the target value is found or determined to be absent.  
  
A binary search is more efficient than a simple search because it reduces the range of possible values by half in each step. In contrast, a simple search sequentially checks every single value step by step. For any list of *n* values, a binary search will take log<sub>2</sub> *n* steps, whereas a simple search will take *n* steps.

### Big O Notation
Big O notation is special notation that tells you how fast an algorithm is. Algorithm speed isn't measured in seconds, but in growth of the number of operations. Therefore, Big O notation tells us how quickly the run time of an algorithm increases as the size of the input increases.  
  
For example, binary search has a run time of O(log *n*) and simple search has a run time of O(*n*). O(log *n*) is faster than O(*n*) and it gets even faster as the list of items you're searching grows.

Here are some commong Big O run times arranged in speed order:
- **O(1)** constant time
- **O(log *n*)** log time
- **O(*n*)** linear time
- **O(*n* log *n*)** log linear time
- **O(*n*<sup>2</sup>)** quadratic time
- **O(*n*!)** factorial time

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
