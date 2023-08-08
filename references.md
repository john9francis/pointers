# References

```cpp
int a = 10;
int &p = a; // It is correct
// but
int &p;
p = a; // It is incorrect as we should declare and initialize references at single step
```

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
