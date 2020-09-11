The `exception::what()` used to get string identifying exception. This function returns a null terminated character sequence that may be used to identify the exception. Below is the syntax for the same:

Header File:
```cpp
#include<exception>
```
Syntax:
```cpp
virtual const char* what() const throw();
```
Return: The function std::what() return a null terminated character sequence that is used to identify the exception.

Note: To make use of std::what(), one should set up the appropriate try and catch blocks.


Below are the programs to understand the implementation of std::what() in a better way:

Program 1:
```cpp
// C++ code for exception::what() 
#include <bits/stdc++.h> 
  
using namespace std; 
  
struct gfg : exception { 
    const char* what() const noexcept 
    { 
        return "GeeksforGeeks!! "
               "A Computer Science"
               " Portal For Geeks"; 
    } 
}; 
  
// main method 
int main() 
{ 
  
    // try block 
    try { 
        throw gfg(); 
    } 
  
    // catch block to handle the errors 
    catch (exception& gfg1) { 
        cout << gfg1.what(); 
    } 
  
    return 0; 
}
```
Output:
```
GeeksforGeeks!! A Computer Science Portal For Geeks
```
Program 2:
```
// C++ code for exception::what() 
  
#include <bits/stdc++.h> 
  
using namespace std; 
  
struct geeksforgeeks : exception { 
    const char* what() const noexcept 
    { 
        return "Hey!!"; 
    } 
}; 
  
// main method 
int main() 
{ 
  
    // try block 
    try { 
        throw geeksforgeeks(); 
    } 
  
    // catch block to handle the errors 
    catch (exception& gfg) { 
        cout << gfg.what(); 
    } 
  
    return 0; 
} 
```
Output:
```
Hey!!
```
Reference: http://www.cplusplus.com/reference/exception/exception/what/
