# Quicksort

## Key Concepts

- Divide & Conquer
- Quicksort
- Big O Notation

## Summary

### Divide & Conquer
Divide & conquer is an approach that involves breaking down a complex problem into smaller and more manageable sub-problems, solving them independently, and then combining their solutions to solve the original problem.  
  
Divide & conquer algorithms are recursive. There are two steps to solving a problem using the approach:
1. Figure out the base case, which is the simplest possible case.
2. Divide or decrease your problem until it becomes the base case.

For example, let's say you have to divide up a piece of land into the largest possible squares such that all squares are the same size. In this example, the base case is when the plot is a perfect square. To decrease the problem, you look at the remaining land when the largest possible square plot is removed.  
  
Suppose the plot of land is 400x240m. The largest possible square is 240x240m, which leaves a 160x240m plot. Now apply the same technique to the remaining plot. The largest possible square is 160x160m, which leaves a 160x80m plot. The largest possible square is 80x80m, which leaves an 80x80m plot. This is the base case since it results in a perfect square. Therefore, the land should be divided into 80x80m squares.

### For Loop vs Recursion
Summing an array can easily be done using a for loop:
```python
def sum(array):
  total = 0
  for item in array:
    total += item
  return total
```
But it can also be done using divide & conquer recursion. The base case is an empty array and the array is decreased by one element with each recursive call.
```python
def sum(array):
  if len(array) == 0: # base case
    return 0
  else:
    return array.pop() + sum(array) # decrease the problem
```

### Quicksort
Quicksort is a divide & conquer sorting algorithm that is faster than the previously discussed selection sort.  
  
Suppose you have an unsorted array. Quicksort will:
1. Pick a number as the pivot.
2. Partition into two subarrays. The first contains all elements greater than the pivot, and the second contains all elements less than the pivot. This divides the problem into three parts: the pivot, an array of elements smaller than the pivot, and an array of elements larger than the pivot.
3. Make a recursive call on the two subarrays.

The base case is an array with length 0 or 1 and the problem is divided into three parts in step 2 above.  
  
This is quicksort's implementation in Python:
```python
def quicksort(array):
  if len(array) <= 1: # base case
    return array
  else: # recursive case; divide the problem
    middle = len(array) // 2
    pivot = array.pop(middle)
    less = [i for i in array if i <= pivot]
    greater = [i for i in array if i > pivot]
    return quicksort(less) + pivot + quicksort(greater)
```

### Big O Notation Revisited
Let's compare a few sorting algorithms using Big O notation.
- Selection Sort: O(*n*^2)
- Quicksort: O(*n*^2) worst case, O(*n* log *n*) average case
- Merge Sort: O(*n* log *n*)

If quicksort is on average as slow as selection sort, why not use merge sort? Because the performance of quicksort depends on the chosen pivot. If a random element is always used as the pivot, the runtime will always be O(*n* log *n*).

Usually constants in Big O notation do not matter, like in the case of binary search's O(log *n*) and simple search's O(*n*^2). However, sometimes, like in the case of merge sort and quicksort, the constant does matter. Quicksort has a smaller constant than merge sort, so quicksort's O(*n* log *n*) is actually faster than merge sort's O(*n* log *n*).

## Exercises

1. **Exercise 4.1**: 
Write out the code for the earlier ```sum``` function.   
*Answer*:
```python
def sum(list):
  if len(list) == 0:
    return 0
  return list.pop() + sum(list)
```

2. **Exercise 4.2**: 
Write a recursive function to count the number of items in a list.  
*Answer*:
```python
def count(list):
  if list == []:
    return 0
  list.pop()
  return 1 + count(list)
```

3. **Exercise 4.3**: 
Find the maximum number in a list.   
*Answer*:
```
def max(list):
  if len(list) == 2:
    return list[0] if list[0] > list[1] else list[1]
  front = list.pop()
  sub_max = max(list)
  return front if front > sub_max else sub_max
```

4. **Exercise 4.4**: 
Remember binary search from chapter 1? It's a divide-and-conquer algorithm, too. Can you come up with the base case and recursive case for binary search?   
*Answer*: The base case for binary search is an array with one item. If the item you're looking for matches the item in the array, you found it! Otherwise, it isn't in the array.  
In the recursive case for binary search, you split the array in half, throw away one half, and call binary search on the other half.

5. **Exercise 4.5**: 
How long would this operation take in Big O notation? Printing the value of each element in an array.  
*Answer*: O(*n*)

6. **Exercise 4.6**: 
How long would this operation take in Big O notation? Doubling the value of each element in an array.  
*Answer*: O(*n*)

7. **Exercise 4.7**: 
How long would this operation take in Big O notation? Doubling the value of just the first element in an array.  
*Answer*: O(1)

8. **Exercise 4.5**: 
How long would this operation take in Big O notation? Creating a multiplication table with all elements in the array. So if your array is [2, 3, 7, 8, 10], you first multiply every element by 2, then multiply every element by 3, then by 7, and so on.  
*Answer*: O(*n*^2)

## Recap

- Divide & conquer works by breaking down a problem into smaller and smaller pieces. If you're using divide & conquer on a list, the base case is probably an empty array or an array with one element.
- If you're implementing quicksort, choose a random element as the pivot. The average runtime of quicksort is O(*n* log *n*).
- The constant in Big O notation can matter sometimes. That's why quicksort is faster than merge sort.
- The constant almost never matters for simple search versus binary search, because O(log *n*) is so much faster than O(*n*) when your list gets big.
