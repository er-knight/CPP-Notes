### `new` operator

**The new operator denotes a request for memory allocation on the Free Store. If sufficient memory is available, new operator initializes the memory and returns the address of the newly allocated and initialized memory to the pointer variable.**

- **Syntax to use new operator: To allocate memory of any data type, the syntax is:**
```
pointer-variable = new data-type;
```
**Here, pointer-variable is the pointer of type data-type. Data-type could be any built-in data type including array or any user defined data types including structure and class.**

- **Example:**
```cpp
/* Pointer initialized with NULL Then request memory for the variable */
int *p = NULL; 
p = new int;   

/*-------------- OR ------------------*/

/* Combine declaration of pointer and their assignment */
int *p = new int; 
```
**Initialize memory: We can also initialize the memory using new operator:**
```
pointer-variable = new data-type(value);
```   
- **Example:**
```cpp
int *p = new int(25);
float *q = new float(75.25);
```
**Allocate block of memory: new operator is also used to allocate a block(an array) of memory of type data-type.**
```
pointer-variable = new data-type[size];
````
**where size(a variable) specifies the number of elements in an array.**

- **Example:**
 ```cpp
 int *p = new int[10]
```
**Dynamically allocates memory for 10 integers continuously of type int and returns pointer to the first element of the sequence, which is assigned to p(a pointer).**
**p[0] refers to first element, p[1] refers to second element and so on.**

### Normal Array Declaration vs Using new
**There is a difference between declaring a normal array and allocating a block of memory using new. The most important difference is, normal arrays are deallocated by compiler (If array is local, then deallocated when function returns or completes). However, dynamically allocated arrays always remain there until either they are deallocated by programmer or program terminates.**

### What if enough memory is not available during runtime?
**If enough memory is not available in the heap to allocate, the new request indicates failure by throwing an exception of type std::bad_alloc, unless “nothrow” is used with the new operator, in which case it returns a NULL pointer (scroll to section “Exception handling of new operator” in this article). Therefore, it may be good idea to check for the pointer variable produced by new before using it program.**

```cpp
int *p = new(nothrow) int;
if (!p)
{
   cout << "Memory allocation failed\n";
}
```

### `delete` operator

**Since it is programmer’s responsibility to deallocate dynamically allocated memory, programmers are provided delete operator by C++ language.**
- **Syntax:**
```
delete pointer-variable;  
```
**Here, pointer-variable is the pointer that points to the data object created by `new`.**
- **Examples:**
```
/* Release memory pointed by p and q */
delete p;
delete q;
```
**To free the dynamically allocated array pointed by pointer-variable, use following form of `delete`:**
```
delete[] pointer-variable;  
```
- **Example:**
```
/* It will free the entire array pointed by p */
delete[] p;
```
- **Example:**
```cpp
#include <iostream> 
using namespace std; 
  
int main () 
{ 
    /* Pointer initialization to NULL */
    int* p = NULL; 
  
    /* Request memory for the variable using new operator */
    p = new(nothrow) int; 
    if (!p) 
        cout << "allocation of memory failed\n"; 
    else
    { 
        /* Store value at allocated address */
        *p = 29; 
        cout << "Value of p: " << *p << endl; 
    } 
  
    /* Request block of memory using new operator */
    float *r = new float(75.25); 
  
    cout << "Value of r: " << *r << endl; 
  
    /* Request block of memory of size n */
    int n = 5; 
    int *q = new(nothrow) int[n]; 
  
    if (!q) 
        cout << "allocation of memory failed\n"; 
    else
    { 
        for (int i = 0; i < n; i++) 
            q[i] = i+1; 
  
        cout << "Value store in block of memory: "; 
        for (int i = 0; i < n; i++) 
            cout << q[i] << " "; 
    } 
  
    /* freed the allocated memory */
    delete p; 
    delete r; 
  
    /* freed the block of allocated memory */
    delete[] q; 
  
    return 0; 
} 
```
**OUTPUT:**
```
Value of p: 29
Value of r: 75.25
Value store in block of memory: 1 2 3 4 5 
```
