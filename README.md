# pointers
Everything you need to know about pointers in C++

# Defining a pointer
```cpp
// Pointers
#include <iostream>
#include <string>
using namespace std;

int main()
{
  int value = 10;
  int* pv = &value;
  cout << "pv: " << pv << "\n";
  cout << "*pv: " << *pv << "\n";
  
  /*
  OUTPUT:
  pv: 0x50528c
  *pv: 10
  */
}
```

# Messing around with pointers pt. 1
```cpp
// Pointers
#include <iostream>
#include <string>
#include <typeinfo>
using namespace std;

void Display(string display, auto value);
void DisplayType(string display, auto value);

int main()
{
  // Defining the variables we are going to use:
  int value;
  int* pvalue;
    
  value = 10;
  Display("value", value);
  Display("value address", &value);
  
  // Changing the value
  value = 11;
  Display("new value", value);
  Display("new value address", &value);
  
  // Defining a pointer
  pvalue = &value;
  Display("pvalue", pvalue);
  Display("*pvalue", *pvalue);
  Display("&pvalue", &pvalue);
  
  // Looking at types
  DisplayType("value type", value);
  DisplayType("&value type", &value);
  DisplayType("pvalue type", pvalue);
  DisplayType("*pvalue type", *pvalue);
  DisplayType("&pvalue type", &pvalue);

  // Changing the original value by changing the pointer
  Display("value", value);
  Display("*pvalue", *pvalue);
  *pvalue = 12;
  Display("new value", value);
  Display("new *pvalue", *pvalue);
  
  // Can we change the address?
  Display("&value", &value);
  Display("pvalue", pvalue);
  pvalue = (int *)0x50548c;
  Display("new &value", &value);
  Display("new pvalue", &value);
  // conclusion: I don't think so...
  
  // How deep can we go?
  int value2;
  int * pvalue2;
  int ** ppvalue2;
  int *** pppvalue2;
  int **** ppppvalue2;
  
  value2 = 2;
  pvalue2 = &value2;
  ppvalue2 = &pvalue2;
  pppvalue2 = &ppvalue2;
  ppppvalue2 = &pppvalue2;
  
  DisplayType("value2 type", value2);
  DisplayType("pvalue2 type", pvalue2);
  DisplayType("*pvalue2 type", *pvalue2);
  DisplayType("ppvalue2 type", ppvalue2);
  DisplayType("*ppvalue2 type", *ppvalue2);
  DisplayType("**ppvalue2 type", **ppvalue2);
  DisplayType("pppvalue2 type", pppvalue2);
  DisplayType("*pppvalue2 type", *pppvalue2);
  DisplayType("ppppvalue2 type", ppppvalue2);
  // conclusion: no limit to how many pointers we can create. 
  

  /*
  OUTPUT
  value: 10
  value address: 0x5054dc
  new value: 11
  new value address: 0x5054dc
  pvalue: 0x5054dc
  *pvalue: 11
  &pvalue: 0x5054d8
  value type: i
  &value type: Pi
  pvalue type: Pi
  *pvalue type: i
  &pvalue type: PPi
  value: 11
  *pvalue: 11
  new value: 12
  new *pvalue: 12
  &value: 0x5054dc
  pvalue: 0x5054dc
  new &value: 0x5054dc
  new pvalue: 0x5054dc
  value2 type: i
  pvalue2 type: Pi
  *pvalue2 type: i
  ppvalue2 type: PPi
  *ppvalue2 type: Pi
  **ppvalue2 type: i
  pppvalue2 type: PPPi
  *pppvalue2 type: PPi
  ppppvalue2 type: PPPPi 
  */
}

void Display(string display, auto value){
  cout << display << ": " << value << '\n';
}

void DisplayType(string display, auto value){
  auto valueType = typeid(value).name();
  cout << display << ": " << valueType << '\n';
}
```

# Pointers in functions can change the original variable
```cpp
// Pointers
#include <iostream>
#include <string>
#include <typeinfo>
using namespace std;

int ChangeValue(int value);
int ReallyChangeValue(int* pvalue);
int DontChangeValue(int* pvalue);

void Display(string display, auto value);
void DisplayType(string display, auto value);

int main()
{
  // Defining the variables we are going to use:
  int value;
  int* pvalue;
  
  // Let's mess around with functions. 
  value = 1;
  
  Display("value before", value);
  Display("changed value", ChangeValue(value));
  Display("value after", value);
  
  // really change value
  pvalue = &value;
  
  Display("value before", value);
  Display("really changed value", ReallyChangeValue(pvalue));
  Display("value after", value);
  // conclusion: if you pass a pointer to a function, it will change it's original value. 
  
  
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

int ChangeValue(int value){
  value += 1;
  return value;
}

int ReallyChangeValue(int* pvalue){
  *pvalue += 1;
  return *pvalue;
}

void Display(string display, auto value){
  cout << display << ": " << value << '\n';
}

void DisplayType(string display, auto value){
  auto valueType = typeid(value).name();
  cout << display << ": " << valueType << '\n';
}
```



# Useful websites:
- [C++ shell: Online C++ compiler](https://cpp.sh/)
- [Defining functions in C++](https://www.tutorialspoint.com/cplusplus/cpp_functions.htm)
