**Syntax:**
```
(pointer_name)->(variable_name)
```
**The arrow operator used to access the members of the structure or the unions using pointers.**  
**Example:**
```cpp
#include<iostream>

class A {
  public: int b;
  A() { b = 5; }
};

int main() {
  A a = A(); // Object of class A
  A* x = &a; // Pointer to the object of class A
  std::cout << "a.b = " << a.b << "\n";
  std::cout << "x->b = " << x->b << "\n";
  return 0;
}
```
