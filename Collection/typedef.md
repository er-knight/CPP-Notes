### `typedef`
You can create a new name for an existing type using typedef. 

Following is the simple syntax to define a new type using typedef −
```cpp
typedef type newname; 
```

For example, the following tells the compiler that feet is another name for int −
```cpp
typedef int feet;
```

Now, the following declaration is perfectly legal and creates an integer variable called distance −
```cpp
feet distance;
```
Example:
```cpp
#include <iostream>
using namespace std;

typedef int feet;

int main() {
  feet distance = 12;
  cout<<distance;
}
```
```
OUTPUT:
12
```
