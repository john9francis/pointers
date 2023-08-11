# References

[home](README.md)

Contents:
- [What is a reference?](#what-is-a-reference)
- [How to define a reference](#how-to-define-a-reference)
- # References are literally the original variable# References are literally the original variable
- # Modifying Values# Modifying Values
- # Be careful with references# Be careful with references
- # Const with references# Const with references
- # Reference to a reference# Reference to a reference
- # References with functions# References with functions
- # Pointer speed vs Reference speed# Pointer speed vs Reference speed
- # Conclusion# Conclusion

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
// Testing pointer vs. reference speed
#include <iostream>

using namespace std;

void Display(string display, auto value){
  /*This function displays the name of a variable and then it's value.*/
  cout << display << ": " << value << '\n';
}


int main() {

  int var1 = 1;
  int var2 = 2;
  
  int& ref1 = var1;
  
  // check the values of everything
  Display("var1", var1);
  Display("&var1", &var1);
  Display("var2", var2);
  Display("&var2", &var2);
  Display("ref1", ref1);
  Display("&ref1", &ref1);
  
  cout << '\n';
  
  // now we will attempt to redefine ref1 to point to var2.
  // We might be expecting this to make ref1 a reference to var2...
  // but this doesn't happen.
  
  ref1 = var2;
  
  Display("var1", var1);
  Display("&var1", &var1);
  Display("var2", var2);
  Display("&var2", &var2);
  Display("ref1", ref1);
  Display("&ref1", &ref1);
  
  /*
  OUTPUT:
  var1: 1
  &var1: 0x50529c
  var2: 2
  &var2: 0x505298
  ref1: 1
  &ref1: 0x50529c

  var1: 2
  &var1: 0x50529c
  var2: 2
  &var2: 0x505298
  ref1: 2
  &ref1: 0x50529c

  */
  
  // conclusion: ref1 will ALWAYS point to var1, and what we did was just
  // redefine var1 to the value of var2. 

}

```

Just remember, **Once you define a reference, you can't redefine it.**

# Const with references
If we want, we can make read-only references using the `const` keyword:
```cpp
int var = 1;
int& rvar = var; // this is a normal reference
const int& rvar = var; // this is a read-only reference.
```

# Reference to a reference

You can make a reference to a reference, and a reference to a reference to a reference. When doing this, all the references are linked together, and when you change one, you change them all. 

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
# References with functions

One unique quality of references is that they always point to the original variable, even in functions.

When you pass a type into a C++ function, it will by default make a copy of that type. If you pass in a reference though, it won't make a copy, it will actually modify the original variable. 

```cpp
// references can modify a value even inside a function
#include <iostream>

using namespace std;

void Display(string display, auto value){
  /*This function displays the name of a variable and then it's value.*/
  cout << display << ": " << value << '\n';
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

We did a similar experiment with pointer in the last tutorial. In my opinion, the references function was easier to code, so let's see if one of them is faster than the other. 

# Pointer speed vs Reference speed

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
From this code we see that pointers and references are the same speed in this context, and references are easier to code.

# Conclusion

References are similar to pointers, but slightly different. In our example, references were actually a bit easier to code. But we can't redefine a reference after we have defined it. References can find the original variable even when passed into a function. In conclusion, references can speed up code and save memory, but we should be careful when using them. 
