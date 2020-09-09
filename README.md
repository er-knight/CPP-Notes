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

An array can also be passed to a function as an argument.  
The parameter should be defined as an array using square brackets, when declaring the function.  
```cpp
#include <iostream>
using namespace std;

int sum(int arr[], int size) {
  int sum = 0;
  for (int i=0; i<size; i++) {
    sum += arr[i];
  }
  return sum;
}

int main() {
  int myarray[] = {3, 4, 5};
  cout<<sum(myarray, 3);
}
```


There are two ways to pass arguments to a function as the function is being called.

- pass by value: This method copies the argument's actual value into the function's formal parameter. Here, we can make changes to the parameter within the function without having any effect on the argument.

Note: formal parameters defined at function definition and actual parameters are passed at function call.

- pass by reference: This method copies the argument's reference into the formal parameter. Within the function, the reference is used to access the actual argument used in the call. This means that any change made to the parameter affects the argument.
```cpp
#include <iostream>
using namespace std;

void func(int *a) {
  *a = 20;
}

int main() {
  int p = 10;
  func(&p);
  cout<<p; // 20
}
```
Note: By default, C++ uses call by value to pass arguments.

**Classes and Objects:**
- characteristics/properties of objects are called attributes.
- each object has its own identity (name), attributes (characteristics) and behavior (methods).
- class is blueprint of its objects.

class structure:
```cpp
class myClass {
 
};
```
Note: A class definition must be followed by a semicolon.

```cpp
#include <iostream>
using namespace std;

class Dog {
  public:
    void sound() {
      cout<<"bhau..bhau..";
    }
};

int main() {
  Dog tommy = Dog(); // creating object - 
  tommy.sound();
}
```
- Abstraction
- Encapsulation (Data Hiding)
- 

Access Specifiers:
- public: attributes and methods specified with public can be accessed outside the class through objects of that class.
- private: attributes and methods specified with public can be accessed only inside the class through objects of that class.
```cpp
#include <iostream>
#include <string>
using namespace std;

class myClass {
  public:
    void setName(string x) {
      name = x;
    }
  private:
    string name;
};

int main() {
  myClass myObj;
  myObj.setName("John");

  return 0;
}
```
Note: If no access specifier is defined, all members of a class are set to private by default.
