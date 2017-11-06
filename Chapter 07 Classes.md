
# Classes

## Basics

```c++
class Student {
  
  // Members
  string name;
  string surname;
  string address;
  
  // Constructors
  public: // Sets everything after this declaration as public; private does the same
  Student() = default;
  Student(const string &s1, const string &s2, const string &s3) :
    name(s1), surname(s2), address(s3) {}  // No semicolumn after this constructor!!!
  
  // Methods
  inline string const getName() {
    return this->name;
  }
  void setName(string newName) {
    (this)->name = newName;
  }
};
```

## Defining Abstract Data Types

**Data abstraction**: programming technique that focuses on the interface to a type. Data abstraction lets programmers ignore the details of how a type is represented and think instead about the operations that the type can perform. Data abstraction is fundamental to both object-oriented and generic programming.

**Encapsulation**: separation of implementation from interface; encapsulation hides the implementation details of a type. In C++, encapsulation is enforced by putting the implementation in the private part of a class.

**Member functions** must be declared inside the class; they may be defined inside the class itself or outside the class body. Nonmember functions that are part of the **interface** are declared and defined outside the class.

**`this`**: Member functions access the object on which they were called through an extra, implicit parameter named `this`. When we call a member function, this is initialized with the address of the object on which the function was invoked.

**`const`**: modifies the type of the implicit this pointer. By default, the type of this is a const pointer to the nonconst version of the class type. Since `this` is implicit and does not appear in the parameter list, there is no place to indicate that this should be a pointer to const. The language resolves this problem by letting us put const after the parameter list of a member function. E.g.:
```c++

```






