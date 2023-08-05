# Intro to pointers:

[home](README.md)

## Contents:
- [Defining a pointer](#defining-a-pointer)
- [Pointers have unique types](#pointers-have-unique-types)
- [Pointer-ception](#pointer-ception)
- [Pointers in functions can change the original variable](#pointers-in-functions-can-change-the-original-variable)
- [Are pointers faster?](#are-pointers-faster)

# What is a pointer?
![pointing finger](point.avif)
A pointer is a variable that "points" to another variable. In more technical terms, a pointer is a variable that holds the address in memory of another variable.

# Defining a pointer

To define a pointer, there are some new symbols that we need to be familiar with:
- `*` The asterisk is used to define a pointer, or get the pointers value
- `&` The ampersand is used to get the address in memory of a variable. 

For example, here's how you would use an asterisk to define a pointer to an int in C++:

```cpp
int* myPointer;
```

Here's how you would get the address of another variable using the ampersand:

```cpp
int myValue = 1;
int* myPointer;

// defining the pointer to point to the value
myPointer = &myValue;
```

Now if we printed out the value of myPointer, we would get some address in memory, like 0x50528c or something like that. 

```cpp
cout << myPointer;
// Output: 0x50528c
```

What if we want to get the value of the pointer? Well, then we use the asterisk again, this time to the left of the value, like so:

```cpp
cout << *myPointer;
// output: 1 
```

Here's a complete example program to define a pointer.

```cpp
// Pointers
#include <iostream>
using namespace std;

int main()
{
  // define a value
  int value = 10;
  
  // define a pointer
  int* pointer = &value;
  
  // display the pointer and the value of the pointer
  cout << "value: " << value << "\n";
  cout << "pointer: " << pointer << "\n";
  cout << "*pointer: " << *pointer << "\n";
  
  /*
  OUTPUT:
  value: 10
  pointer: 0x50528c
  *pointer: 10
  */
}
```

# Pointers have unique types

There are types in C++ such as int, char, float, double, etc. Pointers have their own types as well. For example, if the "int" type was called, "I," the pointer to the int is a type called, "PI." 

To see this in action, here's an example C++ program.

```cpp
// Pointer types
#include <iostream>

using namespace std;

// function to display the type:

void DisplayType(string display, auto value){
  auto valueType = typeid(value).name();
  cout << display << ": " << valueType << '\n';
}

int main()
{
  // define an int value
  int value = 10;
  
  // define a pointer to the int
  int* pointer = &value;
  
  // see the types:
  DisplayType("value type", value);
  DisplayType("pointer type", pointer);
  
  // define a bool value
  bool myBool = true;
  
  // define a pointer to the bool
  bool* pMyBool = &myBool;
  
  // see the types:
  DisplayType("myBool type", myBool);
  DisplayType("pMyBool type", pMyBool);
  
  /*
  OUTPUT:
  value type: i
  pointer type: Pi
  myBool type: b
  pMyBool type: Pb
  */
}
```

# Pointer-ception

![Multiple spider mans pointing to eachother meme](spider-man-meme.jpg)

It is possible to have a pointer to a pointer. You can also have a pointer to a pointer to a pointer. This is generally not reccomended, as it makes code very confusing, but it is possible. 

The interesting thing to me, is the types that are generated. For example, a pointer to a pointer to an int is called a "PPI." A pointer to that would be called a "PPPI." 

As far as I can tell, there is no limit to the depth of "pointer-ception."

```cpp
// Pointer-ception
#include <iostream>
#include <string>
using namespace std;

// function to display the type:

void DisplayType(string display, auto value){
  auto valueType = typeid(value).name();
  cout << display << ": " << valueType << '\n';
}

int main()
{
  // define an int value
  int value = 10;
  
  // define a pointer to the int
  int* pvalue = &value;
  
  // define a pointer to the pointer to the int
  int** ppvalue = &pvalue;
  
  // define a pointer to the pointer to the pointer to the int
  int*** pppvalue = &ppvalue;
  
  // display the types
  DisplayType("value type", value);
  DisplayType("pvalue type", pvalue);
  DisplayType("ppvalue type", ppvalue);
  DisplayType("pppvaue type", pppvalue);
  

  /*
  OUTPUT
  value type: i
  pvalue type: Pi
  ppvalue type: PPi
  pppvaue type: PPPi
  */
}
```


# Pointers in functions can change the original variable

Let's get into some real applications of pointers. One interesting thing about pointers is if you change the value of a pointer, you directly change the original variable's value.

![Marionette doll being controlled by a hand](marionette.png)

This kind of feels like our original value is a marionette doll, and our pointer is like the fingers that control it. We can bring our pointer wherever we want, and it's always attached to that original variable. If we change the pointers value, we change the original variables value. 

Here's a simple example illustrating how changing a pointers value can change the value of a variable. In this example, we have two functions. `ChangeValue()` and `ReallyChangeValue()`. In `ChangeValue()`, we take in an integer, add one, and return the result. In the `ReallyChangeValue()` function, we do the exact same thing but with a pointer. Let's see what happens to the original variable's value when we run both functions.

```cpp
// Pointers changing a value
#include <iostream>
#include <string>
#include <typeinfo>
using namespace std;

int ChangeValue(int value){
  /*This function takes in an int and adds one to it. */
  value += 1;
  return value;
}

int ReallyChangeValue(int* pvalue){
  /*This function takes in an int pointer and adds one to it. */
  *pvalue += 1;
  return *pvalue;
}

void Display(string display, auto value){
  /*This function displays the name of a variable and then it's value.*/
  cout << display << ": " << value << '\n';
}


int main()
{
  // Defining the variables we are going to use:
  int value = 1;
  int* pvalue = &value;
  
  // Let's mess around with functions. 
  
  Display("value before", value);
  Display("changed value", ChangeValue(value));
  Display("value after", value);
  
  // newline
  cout << '\n';
  
  // really change value
  
  Display("value before", value);
  Display("really changed value", ReallyChangeValue(pvalue));
  Display("value after", value);
  
  // conclusion: 
  // if you pass a variable to a function, it creates a copy of the variable.
  // If you pass a pointer to a function, it modifies the original variable.
  
  
  /*
  OUTPUT:
  
  value before: 1
  changed value: 2
  value after: 1
  
  value before: 1
  really changed value: 2
  value after: 2
  */
  
}

```

As you can see by the output, the first function, `ChangeValue()`, creates a copy of the variable, and changes that copy's value, without touching the original variable. The `ReallyChangeValue()` function on the other hand, modifies the original variable.

Can you think of how this could be powerful and efficient? Let's look and see if it's more efficient to use pointers than to not.

# Are pointers faster?

There are two ways of changing a value. One with pointers and one without pointers:
```cpp
// Changing a value in two ways
#include <iostream>
#include <string>
#include <typeinfo>
#include <chrono>
using namespace std;
using namespace std::chrono;

int ChangeValue(int value){
  value += 1;
  return value;
}

void ReallyChangeValue(int* pvalue){
  *pvalue += 1;
}

void Display(string display, auto value){
  cout << display << ": " << value << '\n';
}

int main()
{
  // so there are two ways to change a value:
  // first way:
  cout << "First way \n";
  
  int changeMe = 1;
  Display("before change", changeMe);
  changeMe = ChangeValue(changeMe);
  Display("after change", changeMe);
  
  cout << '\n';
  
  // second way:
  cout << "Second way \n";
  
  changeMe = 1;
  Display("before change", changeMe);
  ReallyChangeValue(&changeMe);
  Display("after change", changeMe);
  
  /*
  OUTPUT:
  First way 
  before change: 1
  after change: 2

  Second way 
  before change: 1
  after change: 2
  */
  
}


```

In the first way, I use the function, "ChangeValue." This function takes the first value, makes a copy of it, adds one to the copy, and returns the copy. Then I assign that returned value to the original value, "changeMe." In the second way, I used the function, "ReallyChangeValue." This takes in a pointer to the "changeMe" variable, and changes it without making a copy.

Making a copy of the variable can be computationally expensive. It's easier on the computer to just change the variable directly. 

## Truck example

![Pickup truck](truck.jpg)

One way to think of these two functions is by imagining you have a friend with a truck. You need to use the truck for a day. Would you rather call and ask them if you can use their truck, or go out and buy your own truck? 

The first way, making a copy of the variable, is like buying our own truck. We have to create a copy of the variable. The second way, using a pointer, is like borrowing the truck. We don't have to make a copy, we just use the value. 

In this very simple example, it's hard to tell a difference in computational speed. Either method is so fast that the difference is negligable. Theoretically though, the pointer method is faster. Let's test that out by looping each method several times, and recording which one is faster.

```cpp
// Testing pointer speed
#include <iostream>
#include <string>
#include <typeinfo>
#include <chrono>

using namespace std;
using namespace std::chrono;

int ChangeValue(int value) {
  value += 1;
  return value;
}

void ReallyChangeValue(int* pvalue) {
  *pvalue += 1;
}

void Display(string display, auto value) {
  cout << display << ": " << value << '\n';
}

int main() {
  int changeMe;

  // Let's loop each method a bunch of times
  int times = 100000000;

  // first method: =======================================================
  changeMe = 1;

  cout << "First method:";

  // keep track of time:
  auto start1 = high_resolution_clock::now();

  // this should take a while
  for (int i = 0; i < times; i++) {
    changeMe = ChangeValue(changeMe);
  }

  // find the time it took to do loop 1
  auto stop1 = high_resolution_clock::now();

  auto duration1 = duration_cast<microseconds>(stop1 - start1).count();
  Display("time spent", duration1);

  // second method: ======================================================
  changeMe = 1;

  cout << "Second method:";

  // keep track of time:
  auto start2 = high_resolution_clock::now();

  // get a pointer to use in the "ReallyChangeValue" function
  int* pchangeMe = &changeMe;

  // the loop
  for (int i = 0; i < times; i++) {
    ReallyChangeValue(pchangeMe);
  }

  // see how much time loop 2 took
  auto stop2 = high_resolution_clock::now();

  auto duration2 = duration_cast<microseconds>(stop2 - start2).count();
  Display("time spent", duration2);

  // display which method went faster
  if (duration1 < duration2) {
    cout << "method 1 was faster.";
  }
  if (duration1 > duration2) {
    cout << "method 2 was faster.";
  }

  /*
  OUTPUT:
  First method:time spent: 840560
  Second method:time spent: 740880
  method 2 was faster. 
  */
  // (Method 2 was consistently faster)
}

```

After looping each method a large amount of times, we found that method 2 was consistenly faster. This speed difference could be very useful when working with very large C++ programs. Any extra efficiency is worth the trouble. 
