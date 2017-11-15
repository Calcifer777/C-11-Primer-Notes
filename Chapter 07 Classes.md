
# Classes

Classes are an expanded concept of data structures: like data structures, they can contain data members, but they can also contain functions as members.

An object is an instantiation of a class. In terms of variables, a class would be the type, and an object would be the variable.

## Basics

```c++
#include <iostream>
#include <string>
using namespace std;

class Student { 
  // Members
  string name;
  int age;
  string address;  
  public: // Sets everything after this declaration as public; private does the same
  // Constructors
  Student() = default;
  Student(const string &s1, const int &i, const string &s2) :
    name(s1), age(i), address(s2) {}  // No semicolumn after this constructor!!! 
  // Methods
  string const getName(); // This member is only declared here; it is defined outside the class
  int const getAge() {return age;}

  Student & setName(string str) {
      name = str;
      return *this;
  }
};

string const Student::getName(){return name;}  //Member definition

void printName(Student s) {
    cout << s.getName();
}
```

## Defining Abstract Data Types

**Data abstraction**: programming technique that focuses on the interface to a type. Data abstraction lets programmers ignore the details of how a type is represented and think instead about the operations that the type can perform. Data abstraction is fundamental to both object-oriented and generic programming.

**Encapsulation**: separation of implementation from interface; encapsulation hides the implementation details of a type. In C++, encapsulation is enforced by putting the implementation in the private part of a class.

### Member Functions

**Member functions** must be declared inside the class; they may be defined inside the class itself or outside the class body. Nonmember functions that are part of the **interface** are declared and defined outside the class.

**`this`**: Member functions access the object on which they were called through an extra, implicit parameter named `this`. When we call a member function, this is initialized with the address of the object on which the function was invoked.

**`const`**: modifies the type of the implicit this pointer. By default, the type of `this` is a const pointer to the nonconst version of the class type. Since `this` is implicit and does not appear in the parameter list, there is no place to indicate that this should be a pointer to const. The language resolves this problem by letting us put const after the parameter list of a member function. E.g.:
```c++
string const getName() {return name;}
// is equivalent to
string Student::getName(const Student *const this) {return this->name;}
```

When defining a member function outside the class body, the member’s definition must match its declaration. The name of a member defined outside the class must include the name of the class of which it is a member (E.g. `getname()`)

When the member function returns the `this` object, the return type must be reference (e.g. : Student& myFunction) and the function must return the current object through the dereference operator (i.e: `return *this;`)

### Constructors

**Synthesized default constructor**: when no constructor is specified, an object of the class is default initialized. For most classes, this synthesized constructor initializes each data member of the class as follows:
- If there is an in-class initializer, use it to initialize the member.
- Otherwise, default-initialize the member.
```c++
Student() = default // No ';' at the end of line!
```

**Constructor Initializer List**: specifies initial values for one or more data members of the object being created.

Best practice: Constructors should not override in-class initializers except to use a different initial value. If you can’t use in-class initializers, each constructor should explicitly initialize every member of built-in type.

```c++
Student(const string &s1, const int &i, const string &s2) :   name(s1), age(i), address(s2) {}
```

With respect to the default initializer, the new parts in these definitions are the colon and the code between it and the curly braces that define the (empty) function bodies. This new part is a constructor initializer list, which specifies initial values for one or more data members of the object being created. The constructor initializer is a list of member names, each of which is followed by that member’s initial value in parentheses (or inside curly braces). Multiple member initializations are separated by commas.

When a member is omitted from the constructor initializer list, it is implicitly initialized using the same process as is used by the synthesized default constructor. In this case, those members are initialized by the in-class initializers.

## Access Control and Encapsulation

Members defined after a `public` specifier are accessible to all parts of the program. The public members define the interface to the class. Members defined after a `private` specifier are accessible to the member functions of the class but are not accessible to code that uses.

If we use the `struct` keyword, the members defined before the first access specifier are public; if we use `class`, then the members are private.

### Friendship

A class can allow another class or function to access its nonpublic members by making that class or function a `friend`. A class makes a function its friend by including a declaration for that function preceded by the keyword `friend`: inside a class definition. To make a friend visible to users of the class, we usually declare each friend (outside the class) in the same header as the class itself.

A class can also make another class its friend or it can declare specific member functions of another (previously defined) class as friends. In addition, a friend function can be defined inside the class body.

**Friendship between classes**

The member functions of a friend class can access all the members, including the nonpublic members, of the class granting friendship. (E.g. `friend class WindowManager`)

Rather than making the entire `WindowManager` class a friend, `Screen` can instead specify that only the clear member is allowed access.

## Additional Class features

In addition to defining data and function members, a class can define its own local names for types, either with `typedef` or with `using`.

Classes often have small functions that can benefit from being inlined. Member functions defined inside the class are automatically `inline`.

As with nonmember functions, member functions may be overloaded so long as the functions differ by the number and/or types of parameters.

**Mutable data members**: Data member that is never const, even when it is a member of a const object. A mutable member can be changed inside a const function.

### Returning this

Example
```c++
Book & setYear(const &int i) {
  year = i;
  return *this;
}
```

When a member returns a reference to the calling object, it is sometimes useful to define another version of that member that handles const objects.

When overloading a (member) function, use private utility functions for common code.

### Class declarations

It is possible to declare a class without defining (e.g. `class Screen;`). This is referred to as **forward declaration**. After a declaration and before a definition is seen, the type `Screen` is an **incomplete type**.

