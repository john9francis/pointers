# Pointers
A beginners guide to pointers in C++

Author: [John Francis](https://github.com/john9francis)

## Contents:
- [Defining a pointer](#defining-a-pointer)
- [Pointers have unique types](#pointers-have-unique-types)
- [Pointer-ception](#pointer-ception)
- [Pointers in functions can change the original variable](#pointers-in-functions-can-change-the-original-variable)
- [Are pointers faster?](#are-pointers-faster)
- [Pointers in Geant4](#pointers-in-geant4)
- [Useful websites](#useful-websites)

# Defining a pointer
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
```cpp
// Pointer types
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
```cpp
// Pointer types
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
```cpp
// Pointers
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

# Are pointers faster?

Two ways of changing a value. One without pointers and one with pointers:
```cpp
// Changing a value with pointers
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
  //return *pvalue;
  // note: the return statement must copy the pointer because it slows the function down a lot.
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

Now let's check to see if pointers are really faster:
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

# pointers in Geant4
It's cool to understand pointers and all, but what's the purpose of using them? To find out, let's disect the pointer use in a more complicated program, Geant4. 

Geant4 is a physics simulation toolkit written in C++. It uses pointers a lot, which saves valuable computational time. 

We are going to dissect the use of pointers in a Geant4 application and see what would happen if we didn't use pointers. 



# Useful websites:
- [C++ shell: Online C++ compiler](https://cpp.sh/)
- [Defining functions in C++](https://www.tutorialspoint.com/cplusplus/cpp_functions.htm)
