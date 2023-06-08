# Selection Sort

## Key Concepts

- Hash Tables
- Hash Functions
- Hash Table Use Cases
- Hash Table Collisons
- Hash Table Performance

## Summary

### Hash Functions
A hash function returns the index of a value, removing the need to perform a search. But there are some requirements for a hash function:
- It needs to be consistent. The same index should be returned every time a value is put in.
- It should map different values to different indexes. Two values should not result in the same index being returned.

A hash function can be combined with an array to store a hash table.

For example, say you want to store the price of an item at the grocery store. You could create a nested array to store the values like this:
```
[["apple", 1.50], ["orange", 2.75], ["milk", 6.50]]
```
Retreiving the price of an item by searching the array would take O(*n*) time if unsorted and O(log *n*) time if sorted. However, by using a hash table, we can eliminate the need to sort.

This is what a hash table would look like in this example:
```
{"apple": 1.50, "apple": 2.75, "milk": 6.50]
```
and the array that the hash table uses would simply look like this:
```
[2.75, 1.50, 6.50]
```
where the hash function returns ```0``` for the value ```"orange"```, ```1``` for the value ```"apple"```, and ```2``` for the value ```"milk"```. 
Searching the array for the price of milk would be instant because the hash function will instantly tell us its index in the array. This is possible because the hash function meets the requirements above. 

If I put ```"apple"``` into the hash function, I will get ```1```. When I retrieve index 1 of the array, I get the price of an apple. All in O(1) constant time!

### Use Cases
Hash tables are good for
- Modeling relationships from one thing to another thing
- Filtering out duplicates
- Caching/memorizing data instead of making your server do work

### Collisions
A collision is when two keys have been assigned the same index by the hash function. It's almost impossible to write a hash function that prevents all collisions.

There are many ways to handle a collision, but the simplest one is to use a linked list at the slot where the collision happens. Let's continue our example from above. 

Let's say a new item is added: avocados. The hash function maps avocados to index 1, which is already occupied by apples. Using the linked list method of handling collisions, index 1 will now point to a linked list that contains the values of apples and avocados. 

Searching for the price of milk or oranges is still instant, but if you search for the price of an avocado or an apple you will need to search through the linked list, decreasing performance.

There are two key takeaways here:
- Your hash function is really important and it should map keys evenly.
- If the linked lists get long, it slows down the hash table a lot, so use a good hash function

#### Performance
The average case for all hash table functions - search, insert, and delete - is O(1). However, the worst case time is O(*n*). The worst case assumes that all values collided to the same index.

To avoid worst case performance, collisions must be avoided. To avoid collisons:
- Have a low load factor. Load factor is the number of items divided by the total number of slots. When the load factor gets too high, the hash table should be resized. The load factor shouldn't be higher than .07.
- Use a good hash function.

Note that programming languages come with build in implementations of hash tables, so you won't need to worry about load factor unless you're implementing a hash table yourself.

## Code Snippets

### Using a hash table to prevent duplicate entries
```python
voted = {}

def check_voter(name):
  if voted.get(name): # if name mapped to a value
    print("Already voted")
  else:
    voted[name] = True
    print("Not yet voted")

check_voter("tom") # => "Not yet voted"
check_voter("mike") # => "Not yet voted"
check_voter("tom") # => "Already voted"
```

### Using hash tables as a cache
```python
cache = {}

def get_page(url):
  if cache.get(url): # if url in cache
    return cache[url] # return cached data
  else: # if url not in cache
    data = get_data_from_server(url) # get the data from the server
    cache[url] = data # save the data in your cache
    return data # return the data
```

## Exercises

1. **Exercise 5.1** 
Is this hash function consistent?   
```f(x) = 1```   
*Answer*: Consistent

2. **Exercise 5.2**
Is this hash function consistent?   
```f(x) = rand()```   
*Answer*: Not consistent

3. **Exercise 5.3**
Is this hash function consistent?   
```f(x) = next_empty_slot()```   
*Answer*: Not consistent

4. **Exercise 5.4**
Is this hash function consistent?   
```f(x) = len(x)```   
*Answer*: Consistent

For the next three exercises, suppose you have these four hash functions that work with strings:  

A. Return "1" for all input.  
B. Use the length of the string as the index.  
C. Use the first character of the string as the index. So, all strings starting with *a* are hashed together, and so on.   
D. Map every letter to a prime number: a = 2, b = 3, c = 5, d = 7, 
e = 11, and so on. For a string, the hash function is the sum of 
all the characters modulo the size of the hash. For example, if 
your hash size is 10, and the string is “bag”, the index is 3 + 2 + 
17 % 10 = 22 % 10 = 2.   

Which hash function would provide a good distribution? Assume a hash table size of 10 slots.

5. **Exercise 5.5**
A phonebook where the keys are names and values are phone numbers. The names are as follows: Esther, Ben, Bob, and Dan.   
*Answer*: Hash functions C and D would give a good distribution.

6. **Exercise 5.6**
A mapping from batter size to power. The sizes are A, AA, AAA, and AAAA.   
*Answer*: Hash functions B and D would give a good distribution.

7. **Exercise 5.7**
A mapping from book titles to authors. The titles are *Maus*, *Fun Home*, and *Watchmen*.   
*Answer*: Hash functions B, C, and D would give a good distribution.

## Recap
- You'll almost never have to implement a hash table yourself since most programming languages provide a built in implementation where you can assume average case performance.
- Hash tables are powerful because they are fast and let you model data in a different way.
- You can make a hash table by combining a hash function with an array.
- Collisions are bad. You need a hash function that minimizes collisions.
- Hash tables have really fast search, insert, and delete.
- Hash tables are good for modeling relationships from one item to another item.
- Once your load factor is greater than .07, it's time to resize your hash table.
- Hash tables are used for caching data (for example, with a web server).
- Hash tables are great for catching duplicates.
