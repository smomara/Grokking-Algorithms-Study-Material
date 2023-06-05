# Recursion

## Key Concepts

- Recursion
- Base Case and Recursive Case
- Stacks

## Summary

### Recursion
Recursion is where a function calls itself. It is an elegant way to solve problems. To explain the concept, the author uses an example:  

#### Example
Suppose you're digging through your grandma's attic and come across a mysterious locked suitcase. 
Grandma tells you that the key for the suitcase is pobably in this other box. 
This box contains more boxes, with more boxes inside those boxes. The key is in a box somewhere. 
What's your algorithm to search for the key?  
  
Here's one approach:
1. Make a pile of boxes to look through
2. Grab a box, and look through it
3. If you find a box, add it to the pile to look through later
4. If you find a key, you're done!
5. Repeat

Here's an alternative approach:
1. Look through the box
2. If you find a box, go to step 1
3. If you find a key, you're done!

The second approach uses recursion. Since the approach goes back to step 1 when a box is found, it is recursive.  
  
There's no performance benefit to recursion, and loops can sometimes be more efficient. However, recursion can be more readable and easier for a programmer to understand. Also, many important algorithms use recursion, so it's important to understand the concept.

### Base Case and Recursive Case
Because a recursive function calls itself, it's easy to write a function incorrectly that ends up in an infinite loop. 
When you write a recursive function, you have to tell it when to stop recursing. That's why every recursive function has two parts: the base case, and the recursive case.  
  
The recursive case is when the function calls itself. The base case is when the function doesn't call itself again, so it doesn't go into an infinite loop. 
In the example above, the recursive case is when a box is found and the base case is when a key is found.

### The Stack
#### Stacks
A stack is a simple data structure with two functions: push and pop. A stack can be thought of conceptually like a stack of sticky notes. The push function is like adding a new item to the top of the stack of sticky notes. The pop function is like removing the sticky note on the top of the stack. Both of these functions have a run time of O(1).

#### The Call Stack
Computers interally use a stack called the call stack to store functions that are currently being run. When a function is called, the computer pushed the function call with its variables in the stack. When a function is called from another function, the called function is pushed to the top of the stack and is executed, meanwhile the calling function is paused in a partially completed state and will be finished when it is back at the top of the stack.  
  
If you call a recursive function, each time the function recurses, it calls itself, pausing the previous function call on the call stack. When the base case is met, each function called in the stack gets popped off and the call stack is resolved all the way back down to the original call of the recursive function.  
  
The call stack is convenient, but can take lots of memory if the stack becomes too tall.

## Exercises

1. **Exercise 3.1**: 
Suppose I show you a call stack like this:

| Call Stack    | Variable | Value  |
| ------------- | -------- | ------ |
| Greet2        | Name     | Maggie |
| Greet         | Name     | Maggie |

What information can you give me, just based on this call stack?  
*Answer*: Here are some things you could tell me:
- The ```greet``` function is called first, with ```name = maggie```
- Then the ```greet``` function calls the ```greet2``` function, with ```name = maggie```
- At this point, the ```greet``` function is in an incomplete suspended state
- The current function call is the ```greet2``` function
- After this function call completes, the ```greet``` function will resume

2. **Exercise 3.2**: 
Suppose you accidentally write a recursive function that runs forever. As you saw, your computer allocates memory on the stack for each function call. What happens to the stack when your recursive function runs forever?  
*Answer*: The stack grows forever. Each program has a limited amount of space on the call stack. When your program runs out of space (which it eventually will), it will exit with a stack-overflow error.

3. **Exercise 2.3**: 
Let’s run a thought experiment. Suppose Facebook keeps a list of usernames. When someone tries to log in to Facebook, a search is done for their username. If their name is in the list of usernames, they can log in. People log in to Facebook pretty often, so there are a lot of searches through this list of usernames. Suppose Facebook uses binary search to search the list. Binary search needs random access - you need to be able to get to the middle of the list of usernames instantly. Knowing this, would you implement the list as an array or a linked list?          
*Answer*: A sorted array. Arrays give you random acess - you can get an element from the middle of the array instantly. You can't do that with linked lists. To get to the middle element in a linked list, you'd have to start at the first element and follow all the linkes down to the middle element.

## Recap

- Recursion is when a function calls itself.
- Every recursive function has two cases: the base case and the recursive case.
- A stack has two operation: push and pop.
- All function calls go onto the call stack.
- The call stack can get very large, which take up a lot of memory.
