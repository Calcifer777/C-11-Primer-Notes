
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

## Class Scope

**Scope and Members Defined outside the Class**

The fact that a class is a scope explains why we must provide the class name as well as the function name when we define a member function outside its class. Outside of the class, the names of the members are hidden. Once the class name is seen, the remainder of the definition—including the parameter list and the function body—is in the scope of the class. As a result, we can refer to other class members without qualification.

**Type Names Are Special**

Ordinarily, an inner scope can redefine a name from an outer scope even if that name has already been used in the inner scope. However, in a class, if a member uses a name from an outer scope and that name is a type, then the class may not subsequently redefine that name. *Definitions of type names usually should appear at the beginning of a class. That way any member that uses that type will be seen after the type name has already been defined*.

## Constructors revisited

If we do not explicitly initialize a member in the constructor initializer list, that member is default initialized before the
constructor body starts executing

Members that are const or references must be initialized. Similarly, members that are of a class type that does not define a default constructor also must be initialized. 

*Use Constructor Initializers
In many classes, the distinction between initialization and assignment is strictly a matter of low-level efficiency: A data member is initialized and then assigned when it could have been initialized directly. More important than the efficiency issue is the fact that some data members must be initialized. By routinely using constructor initializers, you can avoid being surprised by compile-time errors when you have a class with a member that requires a constructor initializer.*

The order of initialization often doesn’t matter. However, if one member is initialized in terms of another, then the order in which members are initialized is crucially important.

->*It is a good idea to write constructor initializers in the same order as
the members are declared. Moreover, when possible, avoid using
members to initialize other members.*

### Delegating constructors

A **delegating constructor** uses another constructor from its own class to perform its initialization. It is said to “delegate” some (or all) of its work to this other constructor.

```c++
class Sales_data {
  public:
  // nondelegating constructor initializes members from corresponding arguments
  Sales_data(std::string s, unsigned cnt, double price):
    bookNo(s), units_sold(cnt), revenue(cnt*price) { }
  // remaining constructors all delegate to another constructor
  Sales_data(): Sales_data("", 0, 0) {}
  Sales_data(std::string s): Sales_data(s, 0,0) {}
  Sales_data(std::istream &is): Sales_data()
  { read(is, *this); }
  // other members as before
};
```

When a constructor delegates to another constructor, the constructor initializer list and function body of the delegated-to constructor are both executed. In Sales_data, the function bodies of the delegated-to constructors happen to be empty. Had the function bodies contained code, that code would be run before control returned to the function body of the delegating constructor.

### The role of the default constructor

`Sales_data obj();` -> although we intended to declare a default-initialized object, `obj` actually declares a function taking no parameters and returning an object of type `Sales_data`. The correct way to define an object that uses the default constructor for  initialization is to leave off the trailing, empty parentheses: `Sales_data obj;`.

### Implicit class-type conversions

**Converting constructors**: A nonexplicit constructor that can be called with a single argument. Such constructors implicitly convert from the argument’s type to the class type.

```c++
string null_book = "9-999-99999-9";
// constructs a temporary Sales_data object
// with units_sold and revenue equal to 0 and bookNo equal to null_book
item.combine(null_book);
```

Here we call the Sales_data combine member function with a string argument. This call is perfectly legal; the compiler automatically creates a Sales_data object from the given string. That newly generated (temporary) Sales_data is passed to combine. Because combine’s parameter is a reference to const, we can pass a temporary to that parameter.

*Try it with constructors that take a cin object to use class objects that are discarded after a function call!*

It is possible to prevent the use of a constructor in a context that requires an implicit conversion by declaring the constructor as `explicit`. The explicit keyword is meaningful only on constructors that can be called with .a single argument. The explicit keyword is used only on the constructor declaration inside the class. It is not repeated on a definition made outside the class body. 

`explicit ` Constructors Can Be Used Only for Direct Initialization
One context in which implicit conversions happen is when we use the copy form of
initialization (with an =) (§ 3.2.1, p. 84). We cannot use an explicit constructor
with this form of initialization; we must use direct initialization

Although the compiler will not use an explicit constructor for an implicit conversion, we can use such constructors explicitly to force a conversion:
```c++
// ok: the argument is an explicitly constructed Sales_data object
item.combine(Sales_data(null_book));
// ok: static_cast can use an explicit constructor
item.combine(**static_cast<Sales_data>**(cin));
```

### Aggregate classes

**Aggregate class**: class with only public data members that has no in-class initializers or constructors. Members of an aggregate can be initialized by a brace-enclosed list of initializers.
```c++
struct Data {
  int ival;
  string s;
};
```

### Literal classes

An aggregate class whose data members are all of literal type is a literal class. A nonaggregate class, that meets the following restrictions, is also a literal class:
• The data members all must have literal type.
• The class must have at least one constexpr constructor.
• If a data member has an in-class initializer, the initializer for a member of built-in type must be a constant expression, or if the member has class type, the initializer must use the member’s own constexpr constructor.
• The class must use default definition for its destructor, which is the member
that destroys objects of the class type

Constexpr constructors 
[Difference between const and constexpr](https://stackoverflow.com/questions/14116003/difference-between-constexpr-and-const)

## Static class Members

The static members of a class exist outside any object; these members are associated with the class, rather than with individual objects of the class type. Objects do not contain data associated with static data members.

Because static data members are not part of individual objects of the class type, they are not defined when we create objects of the class. As a result, they are not initialized by the class’ constructors. Moreover, in general, we may not initialize a static member inside the class. Instead, we must define and initialize each static data member outside the class body.

