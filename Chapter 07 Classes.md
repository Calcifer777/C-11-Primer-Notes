
# Classes

## Basics

```c++
class Student {
  
  // Members
  string name;
  string address;
  int age;
  
  // Constructors
  public: // Sets everything after this declaration as public; private does the same
  Student() = default;
  Student(const string &s1, const int &i, const string &s2) :
    name(s1), surname(i), address(s2) {}  // No semicolumn after this constructor!!!
  
  // Methods
  inline string const getName() {return name;}
  inline string const getAge() {return age;}
  void setName(string newName) {name = newName;}
};
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

When defining a member function outside the class body, the member’s definition must match its declaration. The name of a member defined outside the class must include the name of the class of which it is a member.

When the member function returns the `this` object, the return type must be reference (e.g. : Student& myFunction) and the function must return the current object through the dereference operator (i.e: `return *this;`)

### Constructors

**Synthesized default constructor**: when no constructor is specified, an object of the class is default initialized. For most classes, this synthesized constructor initializes each data member of the class as follows:
- If there is an in-class initializer, use it to initialize the member.
- Otherwise, default-initialize the member.
