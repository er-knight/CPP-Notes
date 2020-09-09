# CPP-Notes

do-while loop:
```cpp
do {
  /* statements; */
} while (/* condition */);
```
Note: There is semicolon (;) after while().

Characters and Strings:
- Character literal is enclosed in single quotes. Ex., 'h'.  
- String literal is enclosed in double quotes, Ex., "harry".

Note: Size of int datatype depends on system architecture. In most modern system architecture, int has minimum size of 4 bytes. 
Generally, short has half of the size of int and long has two-times the size of int.

Note: Size of float datatype depends on system architecture. In most modern system architecture, float has minimum size of 4 bytes. 
Generally, double has two-times the size of float and long double has two-times or four-times the size of float.

**floats are always signed.**

Characters:
A char variable holds a 1-byte integer. However, instead of interpreting the value of the char as an integer, the value of a char variable is typically interpreted as an ASCII character.

If a boolean value is assigned to an integer, true becomes 1 and false becomes 0.
If an integer value is assigned to a Boolean, 0 becomes false and any value that has a non-zero value becomes true.

**Pointer:**
```cpp
int *ptr; // declaring pointer variable
int x = 5;
ptr = &x; // assigning address of a variable to pointer variable
int new_x = *ptr; // dereferencing a pointer (new_x = 5)
```
Note: The asterisk sign can be placed next to the data type, or the variable name, or in the middle.

- address-of operator (&) : returns memory address of its operand.
- contents-of (or dereference) (\*) : returns the value of a variable located at the memory address specified by its operand.

**Static & Dynamic Memory**

In a C++ program, memory is divided into two parts:
- stack: All local variables take up memory from the stack.
- heap: Unused program memory that can be used when the program runs to dynamically allocate the memory.

You can allocate memory at run time within the heap for the variable of a given type using the new operator, which returns the address of the space allocated. 
```cpp
new int;
```
This allocates the memory size necessary for storing an integer on the heap, and returns that address.

-----
```cpp
int *p = new int;
*p = 5;
```
We have dynamically allocated memory for an integer and assigned it a value of 5.
The pointer p is stored in the stack as a local variable and holds the heap's allocated address as its value. The value of 5 is stored at that address in the heap.

-----
For local variables on the stack, managing memory is carried out automatically.
On the heap, it's necessary to manually handle the dynamically allocated memory and use the `delete` operator to free up the memory when it's no longer needed. 
```cpp
delete pointer;
```
This statement releases the memory pointed to by pointer.

```cpp
int *p = new int; // request memory
*p = 5; // store value
cout << *p << endl; // use value
delete p; // free up the memory
```
Forgetting to free up memory that has been allocated with the new keyword will result in memory leaks, because that memory will stay allocated until the program shuts down.

**Dangling Pointers**

The delete operator frees up the memory allocated for the variable, but does not delete the pointer itself, as the pointer is stored on the stack.
Pointers that are left pointing to non-existent memory locations are called dangling pointers.
```cpp
int *p = new int; // request memory
*p = 5; // store value

delete p; // free up the memory
// now p is a dangling pointer

p = new int; // reuse for a new address
```

The NULL pointer is a constant with a value of zero that is defined in several of the standard libraries, including iostream.
It's a good practice to assign NULL to a pointer variable when you declare it, in case you do not have exact address to be assigned. A pointer assigned NULL is called a null pointer. 
```cpp
int *ptr = NULL;
```

Dynamic memory can also be allocated for arrays.
```cpp
int *p = NULL; // Pointer initialized with null
p = new int[20]; // Request memory
delete [] p; // Delete array pointed to by p
```
Note the brackets in the syntax.

Dynamic memory allocation is useful in many situations, such as when your program depends on input. As an example, when your program needs to read an image file, it doesn't know in advance the size of the image file and the memory necessary to store the image.

sizeof() operator:
```cpp
sizeof(expression-or-datatype);
```
Example:
```cpp
cout<<sizeof(int); // 4
```

rand():
```cpp
#include <iostream>
#include <cstdlib>
using namespace std;

int main() {
  cout << rand();
}
```

Note: Use the modulo (%) operator to generate random numbers within a specific range.  
The example below generates whole numbers within a range of 1 to 6.
```cpp
int main () {
  for (int x = 1; x <= 10; x++) {
  cout << 1 + (rand() % 6) << "\n";
  }
}
```
srand():  
The srand() function is used to generate truly random numbers.  
This function allows to specify a seed value as its parameter, which is used for the rand() function's algorithm.  
```cpp
int main () {
  srand(98);

  for (int x = 1; x <= 10; x++) {
    cout << 1 + (rand() % 6) << endl;
  }
}
```
A solution to generate truly random numbers, is to use the current time as a seed value for the srand() function.  
This example makes use of the time() function to get the number of seconds on your system time, and randomly seed the rand() function (we need to include the <ctime> header for it):
  
```cpp
#include <iostream>
#include <cstdlib>
#include <ctime>
using namespace std;

int main () {
  srand(time(0));

  for (int x = 1; x <= 10; x++) {
    cout << 1 + (rand() % 6) << endl;
  }
}
```

time(0) will return the current second count, prompting the srand() function to set a different seed for the rand() function each time the program runs.
Using this seed value will create a different output each time we run the program.

**Function Overloading**

Function overloading allows to create multiple functions with the same name, so long as they have different parameters.

For example, you might need a printNumber() function that prints the value of its parameter.
```cpp
void printNumber(int a) { 
  cout << a;
}
```
This is effective with integer arguments only. Overloading it will make it available for other types, such as floats.
```cpp
void printNumber(float a) { 
  cout << a;
}
```
Now, the same printNumber() function name will work for both integers and floats.  
When overloading functions, the definition of the function must differ from each other by the types and/or the number of arguments in the argument list. 

You can not overload function declarations that differ only by return type.  
The following declaration results in an error.
```cpp
int printName(int a) { }
float printName(int b) { }
double printName(int c) { }
```

Function with same name but different return-type:
```cpp
#include <iostream>

int sum(int a, int b) {
  return a + b;
}

float sum(float a, float b) {
  return a + b;
}

int main() {
  float x = 2.12, y = 3.98;
  
  std::cout <<sum(2, 3)<<"\n"; // 5

  std::cout <<sum(x, y)<<"\n"; // 6.1
}
```
