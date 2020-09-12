### `enum`

- `enum` Creation Syntax:
```cpp
enum enum-name { list of constants };
```
- Different Types `enum` Creations: 
```cpp
#include <iostream>
using namespace std;

enum color { red, green, blue };

int main() {
  cout<<red<<" "<<green<<" "<<blue;
}
```
```
OUTPUT:
0 1 2
```

```cpp
#include <iostream>
using namespace std;

enum color { red, green = 5, blue };

int main() {
  cout<<red<<" "<<green<<" "<<blue;
}
```
```
OUTPUT:
0 5 6
```

```cpp
#include <iostream>
using namespace std;

enum color { red, green, blue } c = blue;

int main() {
  cout<<c;
}
```
```
OUTPUT:
2
```

```cpp
#include <iostream>
using namespace std;

enum color { red, green, blue };
color c = blue;

int main() {
  cout<<c;
}
```
```
OUTPUT:
2
```
