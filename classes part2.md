To be inserted at the BEGINNING of the paragraph:

Classes are an expanded concept of data structures: like data structures, they can contain data members, but they can also contain functions as members.

An object is an instantiation of a class. In terms of variables, a class would be the type, and an object would be the variable.

---------------------------

To be inserted in the constructors paragraph:

With respect to the  default initializer, the new parts in these definitions are the colon and the code between it and the
curly braces that define the (empty) function bodies. This new part is a constructor initializer list, which specifies initial values for one or more data members of the object being created. The constructor initializer is a list of member names, each of which is followed by that member’s initial value in parentheses (or inside curly braces). Multiple member initializations are separated by commas.

When a member is omitted from the constructor initializer list, it is implicitly initialized
using the same process as is used by the synthesized default constructor. In this
case, those members are initialized by the in-class initializers.


*****************

**How opetional arguments are handled**

A constructor that supplies default arguments for all its parameters
also defines the default constructor.

***************************
***************************

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
