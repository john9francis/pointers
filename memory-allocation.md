# Dynamic memory allocation

In C++, we use pointers to control where our variables are stored in memory. This is different from a language like python where all that work is done behind the scenes. 

# Stack vs. Heap

When we run a C++ program, we will need to store information in the computer's RAM. In the RAM, there are two types of memory available to us. There are the stack and the heap.

## Stack
The stack is a stack datastructure, [(1.)](#sources) with a simple but fast system of storing variables. Basically assigning a variable puts it on top of 
the stack, and getting a variable just returns whatever's at the top of the stack. This is called the "LIFO" (last in-first out) method. A few features and drawbacks of stack memory are as follows:
1. Fast
2. Variables must have a known size at compile time

## Heap
The heap is a tree data structure, [(1.)](#sources), [(2.)](#sources)



# sources
1. [Different datastructures in programming](https://john9francis.github.io/datastructures/)
2. [Heap is a tree](https://en.wikipedia.org/wiki/Heap_(data_structure))
