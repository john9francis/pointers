# Dynamic memory allocation

In C++, we use pointers to control where our variables are stored in memory.

# Stack vs. Heap Memory

When we run a C++ program, we will need to store information in the computer's RAM. In the RAM, there are two types of memory available to us. There are the stack and the heap.

## Stack
The stack is a stack datastructure, [(1.)](#sources) with a simple but fast system of storing variables. Basically assigning a variable puts it on top of 
the stack, and getting a variable just returns whatever's at the top of the stack. This is called the "LIFO" (last in-first out) method. A few features and drawbacks of stack memory are as follows:
1. Fast
2. Variables must have a known size at compile time

## Heap
The heap is space available for the program to use during runtime. The pros and cons of heap memory are as follows:
1. Slower
2. Variables can be created and deleted during runtime

- [Bard help on understanding dynamic memory alloc](https://bard.google.com/chat/1d3140fb5ca0d873)


# sources
1. [Different datastructures in programming](https://john9francis.github.io/datastructures/)

# other useful websites
- [Static vs. dynamic memory allocation](https://www.geeksforgeeks.org/difference-between-static-and-dynamic-memory-allocation-in-c/)
- [Dynamic memory alloc in python](https://www.javatpoint.com/python-memory-management) 
