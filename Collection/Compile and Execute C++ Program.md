**Compile and Execute C++ Program**  
Let's look at how to save the file, compile and run the program. 

Please follow the steps given below −
- Open a text editor and type the code in it.
- Save the file as: `filename.cpp`
- Open a command prompt and go to the directory where you saved the file.
- Type `g++ filename.cpp` and press enter to compile your code. If there are no errors in your code the command prompt will take you to the next line and would generate a.out executable file.
- Now, type `a.out` to run your program.

Let's we have a file `hello.cpp` like following:
```cpp
#include <iostream>
using namespace std;

// main() is where program execution begins.
int main() {
   cout << "Hello World"; // prints Hello World
   return 0;
}
```
So, type following commands:
```bash
$ g++ hello.cpp
$ ./a.out
Hello World
```
- You will be able to see `Hello World` printed on the window.
