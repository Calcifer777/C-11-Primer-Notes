# Chapter 2 - Variables and Basic Types

To return the type of a variable/object:
```c++
#include <typeinfo>
...
cout << typeid(var_name).name() << endl;
```

## 2.1 Primitive Built-in Types
### Arithmetic Types

| Type     		| Min. Size		|
| -------------	| ------------- |
| `bool`		| NA 			|
| `char`		| 8 bit 		|
| `wchar_t`		| 16 bits		|
| `char16_t`	| 16 bits		|
| `char32_t`	| 32 bits		|
| `short`		| 16 bits		|
| `int`			| 16 bits		|
| `long`		| 32 bits				|
| `long long`	| 64 bits				|
| `float`		| 6 significant digits	|
| `double`		| 6 significant digits	|
| `long double`	| 6 significant digits	|

An `int` type will be at least as large as `short`; a `long` at least as large as an `int` and so forth.

The types `int`, `short`, `long` and `long long` are signed; add `unsigned` in the declaration command. 

The `unsigned char` type holds values from 0 to 255. `signed char` holds values rom -128 to 127.

### Type Conversion

* Assigning a non-`bool` arithmetic type to a `bool` object, the result is false iff the value is `0`; otherwise `1`. Viceversa, the result is `1` if true, `0` if false.
* Assigning a floating-point value to an integer type truncates the decimal part. Viceversa, the decimal part is set to 0.
* Assigning an out-of-range value to an unsigned type returns remainder of the value modulo the number of values the target type can hold; the value "wraps around" the type ranges.
* Assigning an out-of-range value to a signed type returns undefined (the program might work or crash or produce "wrong" values). Programs that use implementation-defined behavior are called *nonportable*.


In expression that mix signed and unsigned values, the signed values are automatically converted to unsigned.

### Literals

Integer literals can be represented in decimal, octal (leading `0`), and hexadecimal form (`0x`).

  **Character and String Literals**

| Prefix		| Meaning		| Type 		|
| ------------- | ------------- | --------- |
| u 			| Unicode 16 ch | `char16_t`|
| U 			| Unicode 32 ch | `char32_t`|
| L 			| Wide char 	| `wchar_t` |
| u8 			| UTF-8			| `char`	|

  **Integer Literals**

| Suffix		| Type 		|
| ------------- | --------- |
| u or U		| unsigned	|
| l or L		| long		|
| ll or LL		| long long |

  **Floating-Point Literals**

| Suffix		| Type 			|
| ------------- | -------------	|
| f or F		| float 		|
| l or L		| long double	|

The compiler appends a null charachter - `\0` - to character string literals.

**Escape sequences** can be used to represent:
- non-printable characters;
- printable characters using their value (in octal or hexadecimal) within the caracter set used.

For representing numbers in scientific notation, the exponent is indicated by `E` or `e`.

## 2.2 Variables

```c++
int var1, var2, ... ;
long var3;
...
```

Each name in the list of the variable definition has the same *type specifier*.

**Object**: a region of memory the can contain data and has a type.

An object that is **initialized** gets the specified value at the moment it is created. 

**List initialization** : initializes an object enclosing its value in curly brackets. E.g.: `int var_name = {10};`. List initialization will give an error when initializing an object with a value whose built-in type might lead to a loss of information.

When defining a variable without an initializer, the variable is **default initialized**. Each object type establishes whether an object of that type can be defined without an initialized (e.g. the default value of a string is *empty*).
- variables defined outside any function body are initialized by default to 0;
- variables initialized inside a function are **uninitialized**, i.e. their value is undefined.

### Variable Declaration and Definitions

**Separate compilation** : The process of dividing a large program into many smaller source files.

**Declaration** : makes a name known to the program.

**Definition** : creates the associated identity.

In order to declare a variable without defining it, use the `extern` keyword. E.g.
	`int extern var_name;`

### Identifiers

- Can be composed of letters, digits and the underscore character;
- There is no limit  to the length of an identifier;
- Identifiers are case sensitive;
- Identifiers must begin with a letter or an underscore.

### Scope of a Name

*Global scope variable* : accessible throughout the program. Global variables are denoted with the notation `::var_name`

If a local variable has the same name of a global variable, any reference to that name will refer to the local variable, unless `::` is used.

## 2.3 Compound Types

A *compound type* is a type that is defined in terms of another type.

### References

```c++
int &ref_val = variable_name;
```

Define alternative names for objects. A reference must always be initialized. Once initialized the reference is bound to the object and can not be re-assigned.

References are not objects. Therefore, a reference can not be defined to another reference; it can be bound only to an object, not a literal or a more gneral expression.

The type of a reference and the object to which the reference refers must match exactly.

### Pointers

```c++
pointer_type *pointer_name = &reference_object
```

A **pointer** is a compound type that “points to” another type, i.e. whose value is a memory address(sort of). Like references, pointers are used for indirect access to other objects. Unlike a reference, a pointer is an object in its own right. Pointers can be assigned and copied; a single pointer can point to several different objects over its lifetime. 

Unlike a reference, a pointer need not be initialized at the time it is defined. Like other built-in types, pointers defined at block scope have undefined value if they are not initialized.

The type of the pointer must  be the same as the type of the referenced object.

The **pointer value** can be in one of four states:
- it is a valid object;
- it points to the location just immediately after past the end of an object; 
- it is null;
- it is invalid;

In order to return the value of a pointed object, use the **deference operator** `*`. E.g.
```c++
int val = 1;
int *p = &val;
cout << "Ref. object value: " << *p << "\n";
cout << "Pointer value (memory address): " << p << "\n";
```

A **null pointer** does not point to any object. A pointer can be initialized to a nullpointer as
```c++
int *p1 = nullptr;
int *p2 = 0;		\\ must #include cstdlib
int *p3 = NULL; 	\\ NULL is a preprocessor variable
```
Two pointers are equal if they hold the same address and unequal otherwise.

The type `void*` is a special pointer type that can hold the address of any object. `void*`pointers can not be used to change the value of the object to which they point.

A pointer to a pointer is declared by `**`; for 3-level pointers use `***` and so forth. In order to obtain the value  of the pointed object, it is necessary to deference the  pointer with an equal amount of `&`.

### Understanding Compound Type Declarations

#### References to Pointers

```c++
int val = 42;
int *p;				// p points to int
int *&r = p;			// r is a reference (&r); the type of the reference is pointer (*&r); 
				// r refers to a pointer of type int (int * &r)
r = &val;			// p now points to val

cout << "val: " << val << "\n";
cout << "p: " << **&r << "\n";	// these two lines will print the same value
```
## 2.4 `const` Qualifier

`const` is used to fix the value assigned to a variable.

** A `const` object must be initialized**.

```c++ 
const long var_name;
```

When using the same constant variable in multiple files, the `extern` qualifier has to be used both in the initializer and in each of the declarations.

A `const` object may be referenced or pointed only by a `const` reference or a `const` pointer.

### Reference to `const`

```c++
const char var = 'a';
const char &ref = a;
```
Reference to `const` make it impossible to change the value of the bound variable through that reference.

It is possible to initialize a reference to `const` from any expession that can ve converted to the tupe of the reference. It is possible to bind a reference to `const` to:
- a non-`const` object;
- a literal;
- an expression.

It is possible to do so because the compiler bind the reference to `const` to temporary objects, which are the conversions of the value of the referenced value into that of the reference to `const`.

The value of a variable to which a reference to `const` is bound may change.

### Pointers and const

```c++
const double new_var = 7;
const double *ptr = &new_var;
```

As with references, it is possible to use a pointer to `const` to a non-`const` object.

It is possible that a pointer, which is an object, may be constant. In this case, the value to which the pointer is bound may not be changed. Also, as with any `const` object, its value must be initialized.

```c++
float new_var = 1.0;
float * const ptr = &new_var;
```

**Top-level `const` ** : indicates that the pointer itself is constant.

**Low-level `const` ** : indicates that the object to which the pointer is bound is constant.

### `constexpr` and Constant Expressions

A **constant expression** is an expression whose value cannot change and that can be evaluated at compile time (i.e. *before runtime*).

A constant expression can be of one of the following types:
- literal;
- arithmetic;
- reference;
- pointer; in this case the pointer has to be initialized to `nullptr` or `0` or to an object which remains at a fixed address (an object outside a function or, if inside a function, an object such that exists acress calls to a function).

`constexpr` declares a `const` variable and makes sure that it is a constant expression.

With regards to pointers, `constexpr` imposes a top-level `const` to the pointers they address. E.g.:
```c++
constexpr int *p1 = nullptr;

const int var2 = 5;
constexpr int *p2 = &var2;		// these two declarations are legal, as both p1 and p2 are  const pointers
```

## 2.5 Dealing with Types

A **type alias** is a name that is a synonym for another type. 

A type alias can be defined as follows:
- `typedef long long mybignumber;`
- `alias mybignumber = long long`

#### Pointers, *const*, and Type Aliases

`typedef char *mystring;`

indicates that mystring is of type *pointer to char*. Thus, for example, `const mystring cstr = 0` indicates that `cstr` is of type *pointer to char*;

### The `auto` Type Specifier

The type `auto` allows the compiler to deduce the type of the object from that of the initializer. **The resulting type needs not to be the same of the initializer**.

A variable of type auto has to be initialized in its declaration.

- When using a reference as initializer, the initializer is the bound object;
- Top-level `const` are ignored;
- Low-level `const` are kept.

### `decltype` and References

`decltype` returns a reference type for expressions that uield objects that can stand on the left of the assignments.

`decltype((variable))` is always a reference type, but `decltype(variable)` is a reference type only
if variable is a reference. When we apply decltype to a variable without any parentheses, we get the type of that variable. If we wrap the variable’s name in one or more sets of parentheses, the compiler will evaluate the operand as an expression.

[Differences between `auto` and `decltype`](http://thbecker.net/articles/auto_and_decltype/section_01.html)

## 2.6 Defining Data Structures with `struct`

```c++
struct myclass {
	class body
};
```

The class body defines the **members** of that class.

With **data members**, the definition (and default initalization) is the same as normal variables. **In-class initializers** may not be specified inside parentheses.

When a class is defined outside a function, there may be only one definition of that class in any given source file. If a class is used in multiple files, it needs to have the same definition in each of them; in order to ensure that, usually classes - as well as `const` and `constexpr` - are defined in **header files**.


**header guard**: preprocessor variable used to prevent a header from bing included more than once in a single file.

`#define`: defines a name as a preprocessor variable

`ifdef` (`ifndef`): return `TRUE` (`FALSE`) when the input variable is (not) already defined as a preprocessor variable. Every statement that follows is processed until `#endif`.

Preprocessor variables names do not respect C++ scoping rules. They must be unique throughout the program.
