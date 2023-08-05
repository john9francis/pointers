# Pointers and new and delete

[home](README.md)

# What about the new and delete keywords?
New and delete only work with pointers. For example, the following code gives an ERROR:
```cpp
// Dynamic memory
#include <iostream>

using namespace std;


int main() {
  int value = new int;
  value = 1;
  
  delete value;

  /*
  OUTPUT:
  main.cpp:24:7: error: cannot initialize a variable of type 'int' with an rvalue of type 'int *'
  int value = new int;
      ^       ~~~~~~~
  main.cpp:27:3: error: cannot delete expression of type 'int'
  delete value;
  ^      ~~~~~
  2 errors generated.
  */
}
```

This code is how to correctly use the new and delete keywords
```cpp
// Dynamic memory
#include <iostream>

using namespace std;

void Display(string display, auto value) {
  cout << display << ": " << value << '\n';
}

int main() {
  int* value = new int;
  *value = 1;
  
  Display("value", value);
  Display("*value", *value);
  
  delete value;

  /*
  OUTPUT:
  value: 0x505348
  *value: 1
  */
}

```
