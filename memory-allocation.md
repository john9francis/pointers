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


## Nice thing about using dynamic memory
One nice thing about using dynamic memory is we have a pointer that points to that variable. This pointer is really lightweight; just an address to a variable. We can more that pointer around
our program and we don't have to worry about speed as much. For example:

```cpp
MyClass* mc = new MyClass();
myFunction(mc);
```

This function, `myFunction` takes in the pointer to the `MyClass` class. The class might be really big, but it is stored in dynamic memory. We just use the pointer to the class to modify the data. This way, we don't have to make big copies of the data when we move it around, we only need to move around the address. 

# sources
1. [Different datastructures in programming](https://john9francis.github.io/datastructures/)

# other useful websites
- [Static vs. dynamic memory allocation](https://www.geeksforgeeks.org/difference-between-static-and-dynamic-memory-allocation-in-c/)
- [Dynamic memory alloc in python](https://www.javatpoint.com/python-memory-management)
- [C++ documentation for dynamic memory allocation](https://cplusplus.com/doc/tutorial/dynamic/)
