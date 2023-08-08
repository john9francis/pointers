# References
pointers vs references
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
  int value = 1;
  int& rvalue = value;
  
  Display("value", value);
  Display("rvalue", rvalue);
  
  // you can change the value by changing the reference
  rvalue = 2;
  
  Display("value", value);
  Display("rvalue", rvalue);
  
  // Where are they in memory?
  Display("&value", &value);
  Display("&rvalue", &rvalue);
  // in the exact same spot...
  // a reference is just another name for the same variable???
  
  // pointers on the other hand are not in the same spot in memory...
  int value2 = 2;
  int* pvalue2 = &value2;
  
  Display("&value2", &value2);
  Display("&pvalue2", &pvalue2);
  
  /*
  OUTPUT: 
  value: 1
  rvalue: 1
  value: 2
  rvalue: 2
  &value: 0x5052ac
  &rvalue: 0x5052ac
  &value2: 0x505244
  &pvalue2: 0x505240
  */

}

```

be careful with references...
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
  
  // now references
  // int& ref;
  // ref = var;
  //
  // ERROR:
  // main.cpp:35:8: error: declaration of reference variable 'ref' requires an initializer

  // conclusion: you need to initialize a reference
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
