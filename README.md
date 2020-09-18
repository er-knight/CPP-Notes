![](https://github.com/theInvincible/CPP-Notes/blob/master/Collection/c-logo-icon-28389-Windows.ico)

# CPP-Notes

<details>
  <strong>Polymorphism -</strong> function overloading and operator overloading</br>  
  <strong>Deque -</strong> Double ended queue</br>
</details>

[typeid()](https://codeforces.com/blog/entry/16101)  
[Bjarne Stroustrup's C++ Style and Technique FAQ](https://www.stroustrup.com/bs_faq2.html)  
[`const` keyword](https://www.studytonight.com/cpp/const-keyword.php)

do-while loop:
```cpp
do {
  /* statements; */
} while (/* condition */);
```
Note: There is semicolon (;) after while().

**Characters and Strings:**
- Character literal is enclosed in single quotes. Ex., 'h'.  
- String literal is enclosed in double quotes, Ex., "harry".

Note: Size of int datatype depends on system architecture. In most modern system architecture, int has minimum size of 4 bytes. 
Generally, short has half of the size of int and long has two-times the size of int.

Note: Size of float datatype depends on system architecture. In most modern system architecture, float has minimum size of 4 bytes. 
Generally, double has two-times the size of float and long double has two-times or four-times the size of float.

**All numric datatypes are always signed (unless specified unsigned).**

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

**Constructors**

Class constructors are special member functions of a class. They are executed whenever new objects are created within that class.  
The constructor's name is identical to that of the class. It has no return type, not even void.
```cpp
class myClass {
  public:
    myClass() {
      cout <<"Hey";
    }
    void setName(string x) {
      name = x;
    }
    string getName() {
      return name;
    }
  private:
    string name;
};

int main() {
  myClass myObj;
  return 0;
}
```

Now, upon the creation of an object of type myClass, the constructor is automatically called.

Constructors can be very useful for setting initial values for certain member variables.
A default constructor has no parameters. However, when needed, parameters can be added to a constructor. This makes it possible to assign an initial value to an object when it's created, as shown in the following example:
```cpp
class myClass {
  public:
    myClass(string name) {
      setName(name);
    }
    void setName(string x) {
      name = x;
    }
    string getName() {
      return name;
    }
  private:
    string name;
};
int main() {
  myClass ob1("David");
  myClass ob2("Amy");
  cout << ob1.getName();
}
```
We defined a constructor, that takes one parameter and assigns it to the name attribute using the setName() method.
When creating an object, you now need to pass the constructor's parameter, as you would when calling a function.
We've defined two objects, and used the constructor to pass the initial value for the name attribute for each object.
It's possible to have multiple constructors that take different numbers of parameters.

Source & Header Files

The header file (.h) holds the function declarations (prototypes) and variable declarations.
It currently includes a template for our new MyClass class, with one default constructor.
- MyClass.h
```cpp
#ifndef MYCLASS_H
#define MYCLASS_H

class MyClass
{
  public:
    MyClass();
  protected:
  private:
};

#endif // MYCLASS_H
```
The implementation of the class and its methods go into the source file (.cpp).
Currently it includes just an empty constructor.
- MyClass.cpp
```cpp
#include "MyClass.h"

MyClass::MyClass()
{
   //constructor
}
```
The double colon in the source file (.cpp) is called the scope resolution operator, and it's used for the constructor definition.

To use our classes in our main, we need to include the header file.
```cpp
#include <iostream>
#include "MyClass.h"
using namespace std;

int main() {
  MyClass obj;
}
```
The header declares "what" a class (or whatever is being implemented) will do, while the cpp source file defines "how" it will perform those features.

**Destructors**

Destructors are special functions, as well. They're called when an object is destroyed or deleted.
```cpp
class MyClass {
  public: 
    ~MyClass() {
     // some code
    }
};
```

Since destructors can't take parameters, they also can't be overloaded.
Each class will have just one destructor. Defining a destructor is not mandatory, if you don't need one, you don't have to define one.

**#ifndef & #define**

We created separate header and source files for our class, which resulted in this header file.
```cpp
#ifndef MYCLASS_H
#define MYCLASS_H

class MyClass
{
  public:
  MyClass();
  protected:
  private:
};

#endif // MYCLASS_H 
```
ifndef stands for "if not defined". The first pair of statements tells the program to define the MyClass header file if it has not been defined already.
This prevents a header file from being included more than once within one file. endif ends the condition.

Dot Operator

Next, we'll create an object of the type MyClass, and call its myPrint() function using the dot (.) operator:
```cpp
#include "MyClass.h"

int main() {
  MyClass obj;
  obj.myPrint();
}
```

Pointers

We can also use a pointer to access the object's members.
The following pointer points to the obj object:
```cpp
MyClass obj;
MyClass *ptr = &obj;
```
The type of the pointer is MyClass, as it points to an object of that type.

Selection Operator

The arrow member selection operator (->) is used to access an object's members with a pointer.
```cpp
MyClass obj;
MyClass *ptr = &obj;
ptr->myPrint();
```

When working with an object, use the dot member selection operator (.).
When working with a pointer to the object, use the arrow member selection operator (->).

**Constants**

A constant is an expression with a fixed value. It cannot be changed while the program is running.
Use the `const` keyword to define a constant variable. 
```cpp
const int x = 42;
```
All constant variables must be initialized at the time of their creation.

Constant Objects

As with the built-in data types, we can make class objects constant by using the const keyword.
```cpp
const MyClass obj;
```
All const variables must be initialized when they're created. In the case of classes, this initialization is done via constructors. If a class is not initialized using a parameterized constructor, a public default constructor must be provided - if no public default constructor is provided, a compiler error will occur.

Once a const class object has been initialized via the constructor, you cannot modify the object's member variables. This includes both directly making changes to public member variables and calling member functions that set the value of member variables.
When you've used const to declare an object, you can't change its data members during the object's lifetime.

Only non-const objects can call non-const functions.
A constant object can't call regular functions. Hence, for a constant object to work you need a constant function.

To specify a function as a const member, the const keyword must follow the function prototype, outside of its parameters' closing parenthesis. For const member functions that are defined outside of the class definition, the const keyword must be used on both the function prototype and definition. 
- MyClass.h 
```cpp
class MyClass
{
  public:
    void myPrint() const;
};
```
- MyClass.cpp 
```cpp
#include "MyClass.h"
#include <iostream>
using namespace std;

void MyClass::myPrint() const {
  cout <<"Hello"<<endl;
}
```
Now the myPrint() function is a constant member function. As such, it can be called by our constant object:
```cpp
int main() {
  const MyClass obj;
  obj.myPrint();
}
```


Attempting to call a regular function from a constant object results in an error.
In addition, a compiler error is generated when any const member function attempts to change a member variable or to call a non-const member function.
Defining constant objects and functions ensures that corresponding data members cannot be unexpectedly modified.

**Member Initializers**

Recall that constants are variables that cannot be changed, and that all const variables must be initialized at time of creation.
C++ provides a handy syntax for initializing members of the class called the member initializer list (also called a constructor initializer).

Consider the following class: 
```cpp
class MyClass {
  public:
   MyClass(int a, int b) {
    regVar = a;
    constVar = b;
   }
  private:
    int regVar;
    const int constVar;
};
```
This class has two member variables, regVar and constVar. It also has a constructor that takes two parameters, which are used to initialize the member variables.
Running this code returns an error, because one of its member variables is a constant, which cannot be assigned a value after declaration.

In cases like this one, a member initialization list can be used to assign values to the member variables.
```cpp
class MyClass {
 public:
  MyClass(int a, int b)
  : regVar(a), constVar(b)
  {
  }
 private:
  int regVar;
  const int constVar;
};
```
Note that in the syntax, the initialization list follows the constructor parameters. The list begins with a colon (:), and then lists each variable to be initialized, along with the value for that variable, with a comma to separate them.
Use the syntax variable(value) to assign values.
The initialization list eliminates the need to place explicit assignments in the constructor body. Also, the initialization list does not end with a semicolon.

Let's write the previous example using separate header and source files.
- MyClass.h 
```cpp
class MyClass {
  public:
   MyClass(int a, int b);
  private:
   int regVar;
   const int constVar;
};
```
- MyClass.cpp 
```cpp
MyClass::MyClass(int a, int b): regVar(a), constVar(b) {
  cout << regVar << endl;
  cout << constVar << endl;
}
```
We have added cout statements in the constructor to print the values of the member variables.
Our next step is to create an object of our class in main, and use the constructor to assign values.
```
#include "MyClass.h"

int main() {
  MyClass obj(42, 33);
}
/*Outputs 
42
33
*/
```
The member initialization list may be used for regular variables, and must be used for constant variables.
Even in cases in which member variables are not constant, it makes good sense to use the member initializer syntax.

**Composition**

In the real world, complex objects are typically built using smaller, simpler objects. For example, a car is assembled using a metal frame, an engine, tires, and a large number of other parts. This process is called composition.

In C++, object composition involves using classes as member variables in other classes.
This sample program demonstrates composition in action. It contains Person and Birthday classes, and each Person will have a Birthday object as its member.
- Birthday 
```cpp
class Birthday {
 public:
  Birthday(int m, int d, int y): month(m), day(d), year(y) { }
 private:
   int month;
   int day;
   int year;
};
```
Our Birthday class has three member variables. It also has a constructor that initializes the members using a member initialization list.
The class was declared in a single file for the sake of simplicity. Alternatively, you could use header and source files.

Let's also add a printDate() function to our Birthday class: 
```cpp
class Birthday {
 public:
  Birthday(int m, int d, int y): month(m), day(d), year(y) { }
  void printDate() {
   cout<<month<<"/"<<day<<"/"<<year<<endl;
  }
 private:
  int month;
  int day;
  int year;
};
```

Next, we can create the Person class, which includes the Birthday class.
```cpp
#include <string>
#include "Birthday.h"

class Person {
 public:
  Person(string n, Birthday b): name(n),bd(b) { }
 private:
  string name;
  Birthday bd;
};
```
The Person class has a name and a Birthday member, and a constructor to initialize them.
Ensure that the corresponding header files are included.

Now, our Person class has a member of type Birthday:
```cpp
class Person {
 public:
  Person(string n, Birthday b): name(n),bd(b) { }
 private:
  string name;
  Birthday bd;
};
```
Composition is used for objects that share a has-a relationship, as in "A Person has a Birthday".
Let's add a printInfo() function to our Person class, that prints the data of the object: 
```cpp
class Person {
 public:
  Person(string n, Birthday b)
  : name(n),
  bd(b)
  {
  }
  void printInfo()
  {
   cout << name << endl;
   bd.printDate();
  }
 private:
  string name;
  Birthday bd;
};
```
Notice that we can call the bd member's printDate() function, since it's of type Birthday, which has that function defined.

Now that we've defined our Birthday and Person classes, we can go to our main, create a Birthday object, and then pass it to a Person object.
```cpp
int main() {
  Birthday bd(2, 21, 1985);
  Person p("David", bd);
  p.printInfo();
}

/*Outputs
David
2/21/1985
*/
```

We've created a Birthday object for the date of 2/21/1985. Next, we created a Person object and passed the Birthday object to its constructor. Finally, we used the Person object's printInfo() function to print its data.
In general, composition serves to keep each individual class relatively simple, straightforward, and focused on performing one task. It also enables each sub-object to be self-contained, allowing for reusability (we can use the Birthday class within various other classes).

**Friend Functions**

Normally, private members of a class cannot be accessed from outside of that class.
However, declaring a non-member function as a friend of a class allows it to access the class' private members. This is accomplished by including a declaration of this external function within the class, and preceding it with the keyword friend.
In the example below, someFunc(), which is not a member function of the class, is a friend of MyClass and can access its private members.
```cpp
class MyClass {
 public:
  MyClass() {
   regVar = 0;
  }
 private:
  int regVar;
    
  friend void someFunc(MyClass &obj);
};
```
Note that when passing an object to the function, we need to pass it by reference, using the & operator.

The function someFunc() is defined as a regular function outside the class. It takes an object of type MyClass as its parameter, and is able to access the private data members of that object.
```cpp
class MyClass {
 public:
  MyClass() {
   regVar = 0;
  }
 private:
  int regVar;
    
 friend void someFunc(MyClass &obj);
};

void someFunc(MyClass &obj) {
  obj.regVar = 42;
  cout << obj.regVar;
}
```
The someFunc() function changes the private member of the object and prints its value.
To make its members accessible, the class has to declare the function as a friend in its definition. You cannot "make" a function a friend to a class without the class "giving away" its friendship to that function.

Now we can create an object in main and call the someFunc() function:
```cpp
int main() {
  MyClass obj;
  someFunc(obj);
}

//Outputs 42
```

someFunc() had the ability to modify the private member of the object and print its value.

Typical use cases of friend functions are operations that are conducted between two different classes accessing private members of both.
You can declare a function friend across any number of classes.
Similar to friend functions, you can define a friend class, which has access to the private members of another class.

**this keyword**

Every object in C++ has access to its own address through an important pointer called the this pointer.
Inside a member function this may be used to refer to the invoking object.
Let's create a sample class: 
```cpp
class MyClass {
 public:
  MyClass(int a) : var(a)
  { }
 private:
  int var;
};
```
Friend functions do not have a this pointer, because friends are not members of a class. 

The printInfo() method offers three alternatives for printing the member variable of the class. 
```cpp
class MyClass {
 public:
  MyClass(int a) : var(a)
  { }
  void printInfo() {
   cout << var<<endl;
   cout << this->var<<endl;
   cout << (*this).var<<endl; 
  }
 private:
  int var;
};
```
All three alternatives will produce the same result.
this is a pointer to the object, so the arrow selection operator is used to select the member variable.

To see the result, we can create an object of our class and call the member function.
```cpp
#include <iostream>
using namespace std;

class MyClass {
 public:
  MyClass(int a) : var(a)
  { }
  void printInfo() {
   cout << var <<endl;
   cout << this->var <<endl;
   cout << (*this).var <<endl; 
  }
 private:
  int var;
};

int main() {
  MyClass obj(42);
  obj.printInfo();
}

/* Outputs
42
42
42
*/
```

All three of the ways to access the member variable work.
Note that only member functions have a this pointer.

You may be wondering why it's necessary to use the this keyword, when you have the option of directly specifying the variable.
The this keyword has an important role in operator overloading.

**Operator Overloading**

Most of the C++ built-in operators can be redefined or overloaded.
Thus, operators can be used with user-defined types as well (for example, allowing you to add two objects together).

[This](https://api.sololearn.com/DownloadFile?id=2463) chart shows the operators that can be overloaded. Operators that can't be overloaded include :: | .* | . | ?:

Let's declare a sample class to demonstrate operator overloading: 
```cpp
class MyClass {
 public:
  int var;
  MyClass() {}
  MyClass(int a)
  : var(a) { }
};
```
Our class has two constructors and one member variable.
We will be overloading the + operator, to enable adding two objects of our class together.

Overloaded operators are functions, defined by the keyword operator followed by the symbol for the operator being defined.
An overloaded operator is similar to other functions in that it has a return type and a parameter list.

In our example we will be overloading the + operator. It will return an object of our class and take an object of our class as its parameter. 
```cpp
class MyClass {
 public:
  int var;
  MyClass() {}
  MyClass(int a)
  : var(a) { }

  MyClass operator+(MyClass &obj) {
  }
};
```
We need our + operator to return a new MyClass object with a member variable equal to the sum of the two objects' member variables.
```cpp
class MyClass {
 public:
  int var;
  MyClass() {}
  MyClass(int a)
  : var(a) { }

  MyClass operator+ (MyClass &obj) {
   MyClass res;
   res.var= this->var+obj.var;
   return res; 
  }
};
```
Here, we declared a new res object. We then assigned the sum of the member variables of the current object (this) and the parameter object (obj) to the res object's var member variable. The res object is returned as the result.

This gives us the ability to create objects in main and use the overloaded + operator to add them together.
```cpp
int main() {
  MyClass obj1(12), obj2(55);
  MyClass res = obj1+obj2;

  cout << res.var;
}

//Outputs 67
```

With overloaded operators, you can use any custom logic needed. However, it's not possible to alter the operators' precedence, grouping, or number of operands.

**Inheritance**

To demonstrate inheritance, let's create a Mother class and a Daughter class: 
```cpp
class Mother
{
 public:
  Mother() {};
  void sayHi() {
    cout << "Hi";
  } 
};

class Daughter 
{
 public: 
  Daughter() {};
};
```
The Mother class has a public method called sayHi().

This syntax derives the Daughter class from the Mother class.
```cpp
class Daughter : public Mother
{
 public: 
  Daughter() {};
};
```
The Base class is specified using a colon and an access specifier `: public` means, that all public members of the base class are public in the derived class.
In other words, all public members of the Mother class become public members of the Daughter class.

As all public members of the Mother class become public members for the Daughter class, we can create an object of type Daughter and call the sayHi() function of the Mother class for that object:
```cpp
#include <iostream>
using namespace std;

class Mother
{
 public:
  Mother() {};
  void sayHi() {
   cout << "Hi";
  }
};

class Daughter: public Mother
{
 public:
  Daughter() {};
};

int main() {
  Daughter d;
  d.sayHi();
}
//Outputs "Hi"
```

A derived class inherits all base class methods with the following exceptions:
- Constructors, destructors
- Overloaded operators
- The friend functions
A class can be derived from multiple classes by specifying the base classes in a comma-separated list. For example: `class Daughter: public Mother, public Father`

**protected**

There is one more access specifier - protected.
A protected member variable or function is very similar to a private member, with one difference - it can be accessed in the derived classes.
```cpp
class Mother {
 public:
  void sayHi() {
   cout << var;
  }

 private:
  int var=0;

 protected:
  int someVar;
};
```
Now someVar can be accessed by any class that is derived from the Mother class.

**Type of Inheritance**

Access specifiers are also used to specify the type of inheritance.
Remember, we used public to inherit the Daughter class: 
```cpp
class Daughter: public Mother
```
private and protected access specifiers can also be used here.

Public Inheritance: public members of the base class become public members of the derived class and protected members of the base class become protected members of the derived class. A base class's private members are never accessible directly from a derived class, but can be accessed through calls to the public and protected members of the base class.

Protected Inheritance: public and protected members of the base class become protected members of the derived class.

Private Inheritance: public and protected members of the base class become private members of the derived class.
Public inheritance is the most commonly used inheritance type.
If no access specifier is used when inheriting classes, the type becomes private by default.

When inheriting classes, the base class' constructor and destructor are not inherited.
However, they are being called when an object of the derived class is created or deleted.

To further explain this behavior, let's create a sample class that includes a constructor and a destructor:
```cpp
class Mother {
 public:
 Mother() 
 {
  cout <<"Mother ctor"<<endl;
 }
 ~Mother()
 {
  cout <<"Mother dtor"<<endl;
 }
};
```
Creating an object in main results in the following output:
```cpp
int main() {
  Mother m;
}
/* Outputs
Mother ctor
Mother dtor
*/
```
The object is created and then deleted, when the program finishes to run.

Next, let's create a Daughter class, with its own constructor and destructor, and make it a derived class of the Mother:
```cpp
class Daughter: public Mother {
public:
 Daughter()
 {
  cout <<"Daughter ctor"<<endl;
 }
 ~Daughter()
 {
  cout <<"Daughter dtor"<<endl;
 }
};
```
Now, what happens when we create a Daughter object?
```cpp
int main() {
  Daughter m;
}

/*Outputs
Mother ctor
Daughter ctor
Daughter dtor
Mother dtor
*/
```

Note that the base class' constructor is called first, and the derived class' constructor is called next.
When the object is destroyed, the derived class's destructor is called, and then the base class' destructor is called.
You can think of it as the following: The derived class needs its base class in order to work - that is why the base class is set up first.

Constructors
The base class constructor is called first.

Destructors
The derived class destructor is called first, and then the base class destructor gets called.

This sequence makes it possible to specify initialization and de-initialization scenarios for your derived classes.

**Polymorphism**
one function, with different implementations

Polymorphism can be demonstrated more clearly using an example:
Suppose you want to make a simple game, which includes different enemies: monsters, ninjas, etc. All enemies have one function in common: an attack function. However, they each attack in a different way. In this situation, polymorphism allows for calling the same attack function on different objects, but resulting in different behaviors.

The first step is to create the Enemy class.
```cpp
class Enemy {
 protected: 
  int attackPower;
 public:
  void setAttackPower(int a){
   attackPower = a;
  }
};
```
Our Enemy class has a public method called setAttackPower, which sets the protected attackPower member variable.

Our second step is to create classes for two different types of enemies, Ninjas and Monsters. Both of these new classes inherit from the Enemy class, so each has an attack power. At the same time, each has a specific attack function. 
```cpp
class Ninja: public Enemy {
 public:
  void attack() {
   cout << "Ninja! - "<<attackPower<<endl;
  }
};

class Monster: public Enemy {
 public:
  void attack() {
   cout << "Monster! - "<<attackPower<<endl;
  }
};
```
As you can see, their individual attack functions differ.
Now we can create our Ninja and Monster objects in main. 
```cpp
int main() {   
 Ninja n;
 Monster m;  
}
```
Ninja and Monster inherit from Enemy, so all Ninja and Monster objects are Enemy objects. This allows us to do the following:
```cpp
Enemy *e1 = &n;
Enemy *e2 = &m;
```
We've now created two pointers of type Enemy, pointing them to the Ninja and Monster objects.

Now, we can call the corresponding functions:
```cpp
int main() {
  Ninja n;
  Monster m;
  Enemy *e1 = &n;
  Enemy *e2 = &m;

 e1->setAttackPower(20);
 e2->setAttackPower(80);

 n.attack();
 m.attack();
}

/* Output:
Ninja! - 20
Monster! - 80
*/
```

We would have achieved the same result by calling the functions directly on the objects. However, it's faster and more efficient to use pointers.
Also, the pointer demonstrates, that you can use the Enemy pointer without actually knowing that it contains an object of the subclass.

**Virtual Functions**

The previous example demonstrates the use of base class pointers to the derived classes. Why is that useful? Continuing on with our game example, we want every Enemy to have an attack() function.
To be able to call the corresponding attack() function for each of the derived classes using Enemy pointers, we need to declare the base class function as virtual.
Defining a virtual function in the base class, with a corresponding version in a derived class, allows polymorphism to use Enemy pointers to call the derived classes' functions.
Every derived class will override the attack() function and have a separate implementation:
```cpp
class Enemy {
 public:
  virtual void attack() {
  }
};

class Ninja: public Enemy {
 public:
  void attack() {
   cout << "Ninja!"<<endl;
  }
};

class Monster: public Enemy {
 public:
  void attack() {
   cout << "Monster!"<<endl;
 }
};
```
A virtual function is a base class function that is declared using the keyword virtual.

Now, we can use Enemy pointers to call the attack() function.
```
int main() {
  Ninja n;
  Monster m;
  Enemy *e1 = &n;
  Enemy *e2 = &m;

  e1->attack();
  e2->attack();
}

/* Output:
Ninja!
Monster!
*/
```
As the attack() function is declared virtual, it works like a template, telling that the derived class might have an attack() function of its own.

Our game example serves to demonstrate the concept of polymorphism; we are using Enemy pointers to call the same attack() function, and generating different results.
```cpp
e1->attack();
e2->attack();
```
If a function in the base class is virtual, the function's implementation in the derived class is called according to the actual type of the object referred to, regardless of the declared type of the pointer.
A class that declares or inherits a virtual function is called a polymorphic class.

Virtual functions can also have their implementation in the base class: 
```cpp
class Enemy {
 public:
  virtual void attack() {
   cout << "Enemy!"<<endl;
  }
};

class Ninja: public Enemy {
 public:
  void attack() {
   cout << "Ninja!"<<endl;
  }
};

class Monster: public Enemy {
 public:
  void attack() {
   cout << "Monster!"<<endl;
  }
};
```
Now, when you create an Enemy pointer, and call the attack() function, the compiler will call the function, which corresponds to the object's type, to which the pointer points:
```cpp
int main() {
 Ninja n;
 Monster m;
 Enemy e;

 Enemy *e1 = &n;
 Enemy *e2 = &m;
 Enemy *e3 = &e;

 e1->attack();
 // Outputs "Ninja!"

 e2->attack();
 // Outputs "Monster!"

 e3->attack();
 // Outputs "Enemy!"
}
```

This is how polymorphism is generally used. You have different classes with a function of the same name, and even the same parameters, but with different implementations.


Note: When a virtual function is called via base class pointer, it calls those class' function to which the base class pointer points. 

**Pure Virtual Function**

In some situations you'd want to include a virtual function in a base class so that it may be redefined in a derived class to suit the objects of that class, but that there is no meaningful definition you could give for the function in the base class.
The virtual member functions without definition are known as pure virtual functions. They basically specify that the derived classes define that function on their own.
The syntax is to replace their definition by = 0 (an equal sign and a zero): 
```cpp
class Enemy {
 public:
  virtual void attack() = 0;
}; 
```
The = 0 tells the compiler that the function has no body.


A pure virtual function basically defines, that the derived classes will have that function defined on their own.
Every derived class inheriting from a class with a pure virtual function must override that function.
If the pure virtual function is not overridden in the derived class, the code fails to compile and results in an error when you try to instantiate an object of the derived class.

The pure virtual function in the Enemy class must be overridden in its derived classes.
```cpp
class Enemy {
 public:
  virtual void attack() = 0;
};

class Ninja: public Enemy {
 public:
  void attack() {
   cout << "Ninja!"<<endl;
  }
};

class Monster: public Enemy {
 public:
  void attack() {
   cout << "Monster!"<<endl;
  }
};
```

**Abstract Classes**

You cannot create objects of the base class with a pure virtual function.
Running the following code will return an error:
```cpp
Enemy e; // Error
```

These classes are called abstract. They are classes that can only be used as base classes, and thus are allowed to have pure virtual functions.

You might think that an abstract base class is useless, but it isn't. It can be used to create pointers and take advantage of all its polymorphic abilities.
For example, you could write:
```cpp
Ninja n;
Monster m;
Enemy *e1 = &n;
Enemy *e2 = &m;

e1->attack();
e2->attack();
```

In this example, objects of different but related types are referred to using a unique type of pointer (Enemy*), and the proper member function is called every time, just because they are virtual.

**Function Templates**

Functions and classes help to make programs easier to write, safer, and more maintainable.
However, while functions and classes do have all of those advantages, in certain cases they can also be somewhat limited by C++'s requirement that you specify types for all of your parameters.

For example, you might want to write a function that calculates the sum of two numbers, similar to this:
```cpp
int sum(int a, int b) {
  return a+b;
}
```
We can now call the function for two integers in our main.
```cpp
int sum(int a, int b) {
  return a+b;
}

int main () {
  int x=7, y=15;
  cout << sum(x, y) << endl;
}
// Outputs 22
```

The function works as expected, but is limited solely to integers.

It becomes necessary to write a new function for each new type, such as doubles.
```cpp
double sum(double a, double b) {
  return a+b;
}
```
Wouldn't it be much more efficient to be able to write one version of sum() to work with parameters of any type?
Function templates give us the ability to do that!
With function templates, the basic idea is to avoid the necessity of specifying an exact type for each variable. Instead, C++ provides us with the capability of defining functions using placeholder types, called template type parameters.

To define a function template, use the keyword template, followed by the template type definition: 
```cpp
template <class T> 
```
We named our template type T, which is a generic data type.
  
Now we can use our generic data type T in the function:
```cpp
template <class T>
T sum(T a, T b) {
  return a+b;
}

int main () {
    int x=7, y=15;
    cout << sum(x, y) << endl;
}

// Outputs 22
```

The function returns a value of the generic type T, taking two parameters, also of type T.
Our new function worked exactly as the previous one for integer values did.

The same function can be used with other data types, for example doubles:
```cpp
template <class T>
T sum(T a, T b) {
  return a+b;
}

int main () {
  double x=7.15, y=15.54;
  cout << sum(x, y) << endl;
}
// Outputs 22.69
```

The compiler automatically calls the function for the corresponding type.
When creating a template type parameter, the keyword typename may be used as an alternative to the keyword class: 
```cpp
template <typename T>.
```
In this context, the keywords are identical, but throughout this course, we'll use the keyword class.

Template functions can save a lot of time, because they are written only once, and work with different types.
Template functions reduce code maintenance, because duplicate code is reduced significantly.
Enhanced safety is another advantage in using template functions, since it's not necessary to manually copy functions and change types.

Function templates also make it possible to work with multiple generic data types. Define the data types using a comma-separated list.
Let's create a function that compares arguments of varying data types (an int and a double), and prints the smaller one.
```cpp
template <class T, class U>
```
As you can see, this template declares two different generic data types, T and U.

Now we can continue with our function declaration: 
```cpp
template <class T, class U>
T smaller(T a, U b) {
  return (a < b ? a : b);
}
```
The ternary operator checks the a<b condition and returns the corresponding result. The expression (a < b ? a : b) is equivalent to the expression if a is smaller than b, return a, else, return b.

In our main, we can use the function for different data types:
```cpp
template <class T, class U>
T smaller(T a, U b) {
  return (a < b ? a : b);
}

int main () {
  int x=72;
  double y=15.34;
  cout << smaller(x, y) << endl;
}

// Outputs 15
```

The output converts to an integer, because we specified the function template's return type to be of the same type as the first parameter (T), which is an integer.
```cpp
#include <iostream>
using namespace std;

template <class T, class U>
T min(T x, U y) {
  return (x < y ? x : y);
}

int main() {
  cout<<min(12.5, 13)<<"\n";
  cout<<min(14, 13.5);
}
/* output
12.5
13
*/
```

T is short for Type, and is a widely used name for type parameters.
It's not necessary to use T, however; you can declare your type parameters using any identifiers that work for you. The only terms you need to avoid are C++ keywords.
Remember that when you declare a template parameter, you absolutely must use it in your function definition. Otherwise, the compiler will complain!

**Class Templates**

Just as we can define function templates, we can also define class templates, allowing classes to have members that use template parameters as types.
The same syntax is used to define the class template: 
```cpp
template <class T>
class MyClass {

};
```
Just as with function templates, you can define more than one generic data type by using a comma-separated list.


As an example, let's create a class Pair, that will be holding a pair of values of a generic type.
```cpp
template <class T>
class Pair {
 private:
  T first, second;
 public:
  Pair (T a, T b):
   first(a), second(b) {
  }
};
```
The code above declares a class template Pair, with two private variables of a generic type, and one constructor to initialize the variables.

A specific syntax is required in case you define your member functions outside of your class - for example in a separate source file.
You need to specify the generic type in angle brackets after the class name.
For example, to have a member function bigger() defined outside of the class, the following syntax is used: 
```cpp
template <class T>
class Pair {
 private:
  T first, second;
 public:
  Pair (T a, T b):
   first(a), second(b){
  }
  T bigger();
};

template <class T>
T Pair<T>::bigger() {
  // some code
}
```

The bigger function returns the greater value of the two member variables.
```cpp
template <class T>
class Pair {
 private:
  T first, second;
 public:
  Pair (T a, T b):
   first(a), second(b){
  }
  T bigger();
};

template <class T>
T Pair<T>::bigger() {
  return (first>second ? first : second);
}
```

To create objects of the template class for different types, specify the data type in angle brackets, as we did when defining the function outside of the class.
Here, we create a Pair object for integers.
```cpp
Pair <int> obj(11, 22);
cout << obj.bigger();
// Outputs 22
```

We can use the same class to create an object that stores any other type.
```cpp
Pair <double> obj(23.43, 5.68);
cout << obj.bigger();
// Outputs 23.43
```

**Template Specialization**

In case of regular class templates, the way the class handles different data types is the same; the same code runs for all data types.
Template specialization allows for the definition of a different implementation of a template when a specific type is passed as a template argument.

For example, we might need to handle the character data type in a different manner than we do numeric data types.
To demonstrate how this works, we can first create a regular template.
```cpp
template <class T>
class MyClass {
 public:
  MyClass (T x) {
   cout <<x<<" -  not a char"<<endl;
  }
};
```
As a regular class template, MyClass treats all of the various data types in the same way.

To specify different behavior for the data type char, we would create a template specialization.
```cpp
template <class T>
class MyClass {
 public:
  MyClass (T x) {
   cout <<x<<" -  not a char"<<endl;
  }
};

template < >
class MyClass<char> {
 public:
  MyClass (char x) {
   cout <<x<<" is a char!"<<endl;
  }
};
```
First of all, notice that we precede the class name with template<>, including an empty parameter list. This is because all types are known and no template arguments are required for this specialization, but still, it is the specialization of a class template, and thus it requires to be noted as such.

But more important than this prefix, is the <char> specialization parameter after the class template name. This specialization parameter itself identifies the type for which the template class is being specialized (char).
In the example above, the first class is the generic template, while the second is the specialization.
If necessary, your specialization can indicate a completely different behavior from the behavior of the generic template.
  
The next step is to declare objects of different types and check the result:
```cpp
int main () {
  MyClass<int> ob1(42);
  MyClass<double> ob2(5.47);
  MyClass<char> ob3('s');
}
/* Output: 
42 - not a char
5.47 - not a char
s is a char!
*/
```

As you can see, the generic template worked for int and double. However, our template specialization was invoked for the char data type.
Keep in mind that there is no member "inheritance" from the generic template to the specialization, so all members of the template class specializations must be defined on their own. 

**Exceptions**

Problems that occur during program execution are called exceptions.
In C++ exceptions are responses to anomalies that arise while the program is running, such as an attempt to divide by zero.

Throwing Exceptions

C++ exception handling is built upon three keywords: try, catch, and throw.
throw is used to throw an exception when a problem shows up.
For example: 
```cpp
int motherAge = 29;
int sonAge = 36;
if (sonAge > motherAge) {
  throw "Wrong age values";
}
```
The code looks at sonAge and motherAge, and throws an exception if sonAge is found to be the greater of the two.
In the throw statement, the operand determines a type for the exception. This can be any expression. The type of the expression's result will determine the type of the exception thrown.

Catching Exceptions

A try block identifies a block of code that will activate specific exceptions. It's followed by one or more catch blocks. The catch keyword represents a block of code that executes when a particular exception is thrown.
Code that could generate an exception is surrounded with the try/catch block.
You can specify what type of exception you want to catch by the exception declaration that appears in parentheses following the keyword catch.
For example:
```
try {
  int motherAge = 29;
  int sonAge = 36;
  if (sonAge > motherAge) {
   throw 99;
  }
} 
catch (int x) {
  cout<<"Wrong age values - Error Code "<<x;
}

/*Output
"Wrong age values - Error Code 99"
*/
```

The try block throws the exception, and the catch block then handles it.
The error code 99, which is an integer, appears in the throw statement, so it results in an exception of type int.
Multiple catch statements may be listed to handle various exceptions in case multiple exceptions are thrown by the try block.

**Exception Handling**

Exception handling is particularly useful when dealing with user input.
For example, for a program that requests user input of two numbers, and then outputs their division, be sure that you handle division by zero, in case your user enters 0 as the second number.
```cpp
int main() {
  int num1;
  cout <<"Enter the first number:";
  cin >> num1;

  int num2;
  cout <<"Enter the second number:";
  cin >> num2;

  cout <<"Result:"<<num1 / num2;
}
```

This program works perfectly if the user enters any number besides 0.
In case of 0 the program crashes, so we need to handle that input.

In the event that the second number is equal to 0, we need to throw an exception.
```cpp
int main() {
  int num1;
  cout <<"Enter the first number:";
  cin >> num1;

  int num2;
  cout <<"Enter the second number:";
  cin >> num2;

  if(num2 == 0) {
   throw 0;
  } 

  cout <<"Result:"<<num1 / num2;  
}
```

This code throws an exception with the code 0 of type integer.
Next stop: Using the try/catch block to handle the exception!


Now we need to handle the thrown exception using a try/catch block.
```cpp
int main() {
 try {
  int num1;
  cout <<"Enter the first number:";
  cin >> num1;

  int num2;
  cout <<"Enter the second number:";
  cin >> num2;

  if(num2 == 0) {
   throw 0;
  } 

  cout <<"Result:"<<num1 / num2; 
 }
 catch(int x) {
  cout <<"Division by zero!";
 }
}
```

This results in the output of "Division by zero!" as an alternative to a program crash, when 0 is entered as the second number.

In our case, we catch exceptions of type integer only. It's possible to specify that your catch block handles any type of exception thrown in a try block. To accomplish this, add an ellipsis (...) between the parentheses of catch: 
```cpp
try {
  /*statements */ 
} catch(...) {
  /*statements */ 
}
```
Note: Any type of value can be used in the catch block of exceptions.

**Working with Files**

Another useful C++ feature is the ability to read and write to files. That requires the standard C++ library called fstream.
Three new data types are defined in fstream:
ofstream: Output file stream that creates and writes information to files.
`ifstream`: Input file stream that reads information from files.
`fstream`: General file stream, with both ofstream and ifstream capabilities that allow it to create, read, and write information to files.

To perform file processing in C++, header files <iostream> and <fstream> must be included in the C++ source file.
```cpp
#include <iostream>
#include <fstream>
```
These classes are derived directly or indirectly from the classes istream and ostream. We have already used objects whose types were these classes: cin is an object of class istream and cout is an object of class ostream.
  
**Opening a File**

A file must be opened before you can read from it or write to it.
Either the ofstream or fstream object may be used to open a file for writing.
Let's open a file called "test.txt" and write some content to it: 
```cpp
#include <iostream>
#include <fstream>
using namespace std;

int main() {
  ofstream MyFile;
  MyFile.open("test.txt");

  MyFile << "Some text. \n";
}
```
The above code creates an ofstream object called MyFile, and uses the open() function to open the "test.txt" file on the file system. As you can see, the same stream output operator is used to write into the file.
If the specified file does not exist, the open function will create it automatically.

**Closing a File**

When you've finished working with a file, close it using the member function close().
```cpp
#include <iostream>
#include <fstream>
using namespace std;

int main() {
  ofstream MyFile;
  MyFile.open("test.txt");

  MyFile << "Some text! \n";
  MyFile.close();
}
```
Running this code will cause a "test.txt" file to be created in the directory of your project with "Some text!" written in it.
You also have the option of specifying a path for your file in the open function, since it can be in a location other than that of your project.

You can also provide the path to your file using the ofstream objects constructor, instead of calling the open function.
```cpp
#include <fstream>
using namespace std;

int main() {
  ofstream MyFile("test.txt");

  MyFile << "This is awesome! \n";
  MyFile.close();
}
```
As with the open function, you can provide a full path to your file located in a different directory.

Under certain circumstances, such as when you don't have file permissions, the open function can fail.
The `is_open()` member function checks whether the file is open and ready to be accessed.
```cpp
#include <iostream>
#include <fstream>
using namespace std;

int main() {
  ofstream MyFile("test.txt");

  if (MyFile.is_open()) {
   MyFile << "This is awesome! \n";
  }
  else {
   cout << "Something went wrong";
  }
  MyFile.close();
}
```
The `is_open()` member function checks whether the file is open and ready to be accessed.

**File Opening Modes**

An optional second parameter of the open function defines the mode in which the file is opened. This list shows the supported modes.
| Mode Parameter | Meaning |
| :------------: |---------|
| `ios::app` | append to end of file |
| `ios::ate` | go to end of file on opening | 
| `ios::binary` | file open in binary mode |
| `ios::in` | open file for reading only |
| `ios::out` | open file for writing only |
| `ios::trunc` | delete contents of a file if it exists | 

All these flags can be combined using the bitwise operator OR (|).
For example, to open a file in write mode and truncate it, in case it already exists, use the following syntax:
```cpp
ofstream outfile;
outfile.open("file.dat", ios::out | ios::trunc );
```

**Reading from a File**

You can read information from a file using an ifstream or fstream object.
```cpp
#include <iostream>
#include <fstream>
using namespace std;

int main () {
  string line;
  ifstream MyFile("test.txt");
  while ( getline (MyFile, line) ) {
   cout << line << '\n';
  }
  MyFile.close();
}
```
The getline function reads characters from an input stream and places them into a string.
The example above reads a text file and prints the contents to the screen.
Our while loop uses the getline function to read the file line by line.
