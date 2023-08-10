# References

[home](README.md)

Contents:
- [What is a reference?](#what-is-a-reference)

# What is a reference?
A reference is similar to a pointer, but a little bit different. Where a pointer is the address to a variable, a reference IS the variable. It's not a copy of the variable, it actually is the variable. In more technical terms, a reference is a variable that is located in the same exact memory address as the original variable. 

![Man looking in the mirror](mirror.jpg)

# How to define a reference

To define a reference, we use the ampersand, "`&`". Here's an example of creating a reference to a variable.
```cpp
int var = 1;
int& rvar = var;
``` 
Note: You can't initialize a reference and then assign it later... You have to assign a reference to a variable on the same line you create it. So the following code will produce an ERROR:
```cpp
int& rvar;
rvar = var; // NOPE, you gotta do it in the same line
```

# References are literally the original variable
To prove that a reference is in fact the original variable and not a copy, consider this code:
```cpp
// References
#include <iostream>

using namespace std;

void Display(string display, auto value){
  /*This function displays the name of a variable and then it's value.*/
  cout << display << ": " << value << '\n';
}

void DisplayType(string display, auto value){
  /*This function displays the name of the value and then it's type */
  auto valueType = typeid(value).name();
  cout << display << ": " << valueType << '\n';
}

int main() {
  
  int var = 1;
  int& rvar = var;
  
  // display the value of both variables
  Display("var", var);
  Display("rvar", rvar);
  
  // display the location in memory of both variables
  Display("&var", &var);
  Display("&rvar", &rvar);
  
  // display the types of both var and rvar
  DisplayType("var", var);
  DisplayType("rvar", rvar);
  
  // display if var == rvar
  if (var == rvar){
    cout << "True";
  }
  else{
    cout << "False";
  }
  
  /*
  OUTPUT:
  var: 1
  rvar: 1
  &var: 0x5052f8
  &rvar: 0x5052f8
  var: i
  rvar: i
  True 
  */
  
  // conclusion: var and rvar are the exact same variable with different names. 
  
}

```

# Modifying Values

If you modify a value, you also modify any references to that value. If you modify a reference, you also modify the original value.

```cpp
// Testing pointer vs. reference speed
#include <iostream>

using namespace std;

void Display(string display, auto value){
  /*This function displays the name of a variable and then it's value.*/
  cout << display << ": " << value << '\n';
}

void DisplayType(string display, auto value){
  /*This function displays the name of the value and then it's type */
  auto valueType = typeid(value).name();
  cout << display << ": " << valueType << '\n';
}

int main() {
  int var = 1;
  int& rvar = var;
  
  Display("var", var);
  Display("rvar", rvar);
  
  var = 2;
  
  Display("var", var);
  Display("rvar", rvar);
  
  rvar = 3;
  
  Display("var", var);
  Display("rvar", rvar);
  
  /*
  OUTPUT:
  var: 1
  rvar: 1
  var: 2
  rvar: 2
  var: 3
  rvar: 3
 
  */
}

```

# Be careful with references

With pointers, you can change the value of a pointer at any time to another variable. With references however, you define it once and that's it. If you try to reassign a reference to another variable, you will end up redefining the variable that the reference points to. For example:

```cpp
int var1 = 1;
int var2 = 2;

int& ref1 = var1; // ref1 = 1.

// attempting to redefine ref1 to be a reference to variable 2
ref1 = var2; // ref1 = 2, and now var1 = 2! bad news!
```

Just remember, **Once you define a reference, you can't redefine it.**

```cpp
// References
#include <iostream>

using namespace std;

void Display(string display, auto value){
  /*This function displays the name of a variable and then it's value.*/
  cout << display << ": " << value << '\n';
}

int main()
{
  int* ptr;
  int var = 7;
  int foo = 21;
  
  ptr = &var;
  
  Display("ptr", ptr);
  Display("*ptr", *ptr);
  
  ptr = &foo;
  
  Display("ptr", ptr);
  Display("*ptr", *ptr);
  
  ptr = &var;
  
  Display("ptr", ptr);
  Display("*ptr", *ptr);
  
  // conclusion: you can point a pointer wherever
  
  Display("var", var);
  Display("foo", foo);
  
  int& ref = var;
  
  Display("ref", ref);
  Display("&ref", &ref);
  
  ref = foo;
  
  Display("ref", ref);
  Display("&ref", &ref);
  
  Display("var", var);
  Display("foo", foo);
  
  // conclusion: BE CAREFUL WITH REFERENCES...
  // You can overwrite another variable with a reference if you try and reassign a reference
  
  /*
  OUTPUT:
  ptr: 0x505298
  *ptr: 7
  ptr: 0x505294
  *ptr: 21
  ptr: 0x505298
  *ptr: 7
  var: 7
  foo: 21
  ref: 7
  &ref: 0x505298
  ref: 21
  &ref: 0x505298
  var: 21
  foo: 21
 
  */

}
```

* I feel like i'm starting to see the possibilities of references... and the importance of the "const" keyword, lol. 
* So what's the point of a reference? It's literally just another name for the exact same place in memory...

```cpp
// References are the exact same variable as the original
#include <iostream>

using namespace std;

void Display(string display, auto value){
  /*This function displays the name of a variable and then it's value.*/
  cout << display << ": " << value << '\n';
}

void DisplayType(string display, auto value){
  auto valueType = typeid(value).name();
  cout << display << ": " << valueType << '\n';
}

int main()
{
  int value = 1;
  int value2 = value;
  int& rvalue = value;
  
  Display("value", value);
  Display("value2", value2);
  Display("rvalue", rvalue);
  
  Display("&value", &value);
  Display("&value2", &value2);
  Display("&rvalue", &rvalue);

  /*
  OUTPUT:
  value: 1
  value2: 1
  rvalue: 1
  &value: 0x50529c
  &value2: 0x505298
  &rvalue: 0x50529c
  */
}

```
references don't have unique types:
```cpp
// References don't have unique types
#include <iostream>

using namespace std;

void Display(string display, auto value){
  /*This function displays the name of a variable and then it's value.*/
  cout << display << ": " << value << '\n';
}

void DisplayType(string display, auto value){
  auto valueType = typeid(value).name();
  cout << display << ": " << valueType << '\n';
}

int main()
{
  int value = 1;
  int& rvalue = value;
  
  DisplayType("value", value);
  DisplayType("rvalue", rvalue);
  
  /*
  OUTPUT:
  value: i
  rvalue: i
  */
}

```

You can make a reference to a reference
```cpp
// Reference to a reference?
#include <iostream>

using namespace std;

void Display(string display, auto value){
  /*This function displays the name of a variable and then it's value.*/
  cout << display << ": " << value << '\n';
}

void DisplayType(string display, auto value){
  auto valueType = typeid(value).name();
  cout << display << ": " << valueType << '\n';
}

int main()
{
  // you can define a reference to a reference
  int value = 1;
  int& rvalue = value;
  int& rrvalue = rvalue;
  
  Display("value", value);
  Display("rvalue", rvalue);
  Display("rrvalue", rrvalue);
  
  // they are all the exact same variable
  Display("&value", &value);
  Display("&rvalue", &rvalue);
  Display("&rrvalue", &rrvalue);
  
  // changing one value changes them all
  rrvalue = 2;
  
  Display("value", value);
  Display("rvalue", rvalue);
  Display("rrvalue", rrvalue);
  
  rvalue = 3;
  
  Display("value", value);
  Display("rvalue", rvalue);
  Display("rrvalue", rrvalue);

  /*
  OUTPUT:
  value: 1
  rvalue: 1
  rrvalue: 1
  &value: 0x50529c
  &rvalue: 0x50529c
  &rrvalue: 0x50529c
  value: 2
  rvalue: 2
  rrvalue: 2
  value: 3
  rvalue: 3
  rrvalue: 3
  */
}

```
references with functions
```cpp
// references can modify a value even inside a function
#include <iostream>

using namespace std;

void Display(string display, auto value){
  /*This function displays the name of a variable and then it's value.*/
  cout << display << ": " << value << '\n';
}

void DisplayType(string display, auto value){
  auto valueType = typeid(value).name();
  cout << display << ": " << valueType << '\n';
}

void ChangeValue(int value){
  value += 1;
}

void ReallyChangeValue(int& value){
  value += 1;
}

int main()
{
  int value = 1;
  
  Display("value", value);
  ChangeValue(value);
  Display("value", value);
  
  cout << '\n';
  
  Display("value", value);
  ReallyChangeValue(value);
  Display("value", value);

  /*
  OUTPUT:
  value: 1
  value: 1

  value: 1
  value: 2
  */

}

```
^^ This way is actually easier than the similar thing with pointers

testing pointer speed vs reference speed with functions

```cpp
// Testing pointer vs. reference speed
#include <iostream>

#include <chrono>

using namespace std;
using namespace std::chrono;

int ChangeValue(int value) {
  value += 1;
  return value;
}

void pReallyChangeValue(int* pvalue) {
  *pvalue += 1;
}

void rReallyChangeValue(int& rvalue) {
  rvalue += 1;
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
    pReallyChangeValue(pchangeMe);
  }

  // see how much time loop 2 took
  auto stop2 = high_resolution_clock::now();

  auto duration2 = duration_cast<microseconds>(stop2 - start2).count();
  Display("time spent", duration2);

  // display which method went faster
  //if (duration1 < duration2) {
  //    cout << "method 1 was faster.";
  //}
  //if (duration1 > duration2) {
  //    cout << "method 2 was faster.";
  //}
  
  // third method: references ===============================================
   changeMe = 1;

  cout << "Third method:";

  // keep track of time:
  auto start3 = high_resolution_clock::now();

  // get a reference to use in the "ReallyChangeValue" function
  int& rchangeMe = changeMe;

  // the loop
  for (int i = 0; i < times; i++) {
    rReallyChangeValue(rchangeMe);
  }

  // see how much time loop 2 took
  auto stop3 = high_resolution_clock::now();

  auto duration3 = duration_cast<microseconds>(stop3 - start3).count();
  Display("time spent", duration2);

  // display which method went fastest
  if (duration1 < duration2 && duration1 < duration3) {
    cout << "method 1 was fastest.";
  }
  if (duration2 < duration1 && duration2 < duration3) {
    cout << "method 2 was fastest.";
  }
  if (duration3 < duration1 && duration3 < duration2) {
    cout << "method 3 was fastest.";
  }
  /*
  OUTPUT:
  First method:time spent: 1122560
  Second method:time spent: 1018840
  Third method:time spent: 1018840
  method 3 was fastest. 
  */
  // second and third method were consistently tied for fastest
}

```
conclusion: pointers and references are the same speed in this context, and references are easier.
