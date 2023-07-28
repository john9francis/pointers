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



# Useful websites:
- [C++ shell: Online C++ compiler](https://cpp.sh/)
- [Defining functions in C++](https://www.tutorialspoint.com/cplusplus/cpp_functions.htm)
