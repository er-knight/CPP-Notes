```cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
  string s = "abcde";
  cout<<s<<"\n";
  s.erase(s.begin() + 2);
  cout<< s;
}
```
```
OUTPUT:
abcde
abcd
```
