# Functions

## Basics

**Local variables** Variables defined inside a block.

**Automatic object**: an object that exists only while a block is executing. Automatic objects corresponding to local
variables are initialized if their definition contains an initializer. Otherwise, they are default initialized, which means that uninitialized local variables of built-in type have undefined values.

**Local static object**: local objects whose value persists across calls to the function. Local static objects that are created and initialized before control reaches their use and are destroyed when the program ends.

**Function declaration (prototypes)**: `returnType functionName(typeP1 p1, typeP2 p2 ...);` . The header that declares a function should be included in the source file that defines that function.

## Argument Passing

### Passing Arguments by Value

Passing an argument by value works exactly the same way; nothing the function does to the parameter can affect the argument.

**Pointer parameters**
If the argument of a function is a pointer to a variable and the value associated to that variable is changed through that pointer within the function, the value will be changed for the outside variable too.

``` c++ 
  void reset(int *p) {
    *p = 0;
  }
  
  int i = 42;
  reset(&i) = 0; // Yields i = 0
```

### Passing Arguments by Reference

``` c++ 
  void reset(int &r) {
    r = 0;
  }
  
  int i = 42;
  reset(i) = 0; // Yields i = 0
```

Passing arguments by reference can be used to make a function return more than one value. The variables containing additional values can be passed as references to the function.

**Using a reference instead of a reference to const limits the type of arguments that can be used with the function. We cannot pass a const object, or a literal, or an object that requires conversion to a plain reference parameter.**

##### Passing arrays

If we pass an array to print, that argument is automatically converted to a pointer to the first element in the array; the size of the array is irrelevant.

Options to use for cycling through array elements
- Using a Marker to Specify the Extent of an Array: good for strings; bad for int[]
```c++
void print(const char *cp)
{
if (cp) // if cp is not a null pointer
while (*cp) // so long as the character it points to is not a null character
cout << *cp++; // print the character and advance the pointer
}
```
- Using the Standard Library Conventions
```c++
void print(const int *beg, const int *end)
{
// print every element starting at beg up to but not including end
while (beg != end)
cout << *beg++ << endl; // print the current element and advance the pointer
}
```
- Explicitly Passing a Size Parameter: size is passed explicitly and used to control access to elements
```c++
// const int ia[] is equivalent to const int* ia
void print(const int ia[], size_t size)
{for (size_t i = 0; i != size; ++i) {
  cout << ia[i] << endl;
}
```

**Array Reference Parameters**: need to specify the size parameter!
```c++
void print(int (&arr)[10])
{ 
  for (auto elem :arr)
  cout << elem << endl;
}
```

**Passing a Multidimensional Array**: As with any array, a multidimensional array is passed as a pointer to its first element. Because we are dealing with an array of arrays, that element is an array, so the pointer is a pointer to an array. The size of the second (and any subsequent) dimension is part of the element type and must be specified

#### Functions with varying parameters

**Initializer_list**

It is used to let a function have an unknown number of parameters of the same type. Thus an initializer_list object represents an array of elements of the same type, and it is contained in the initializer_list header.

| Code | Result |
| ---- | ------ |
| initializer_list<T> lst;                | Default initialization. Creates an empty list of type T elements |
| initializer_list<T> lst{a, b, ...};     | lst has many elements as there are initializers. Elements are copies of the corresponding initializers. Elements are const | 
| lst2 = lst1; lst2(lst1);  | When a list is initialized from another, the two of them share the same elements |
| lst.size(); | Returns the number of elements in the list |
| lst.begin(); lst.end() | Pointers to the first and one after the last elements of  the  list |

```c++
int sum(initializer_list<int> &list) {
    int sum = 0;
    for (auto e : list)
        sum += e;
    return  sum;
}

int main()
{
    initializer_list<int> lst = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
    cout<<sum(lst);
    return 0;
}
```

**Ellipsis Parameters**

Allow a C++ program to interface with a C program. An ellipsis parameter may appear only as the last element in a parameter list and may take either of two forms:
```c++
void foo(parm_list, ...); // or
void foo(...);
```
No type checking is done for the arguments that correspond to the ellipsis parameter.

## Return types and the `return` Statement

### Functions that return no values

```c++
return;
```

### Functions that return a value

A function can not return an array type or a function type, but it can return a pointer to array or a pointer to a function.

```c++
int sum(const int a, const int b);
```

**List initializing the return value**

```c++
vector<int> createVec() {
    return {1, 2, 3};
}
```

**Recursive functions**
```c++
int factorial(int n) {
    if (n<0)
        return -1;
    else if (n==0 || n==1)
        return 1;
    else
        return n * factorial(n-1);
}
```

#### Returning references
```c++
const char& firstChar(const string &str) {
    return str[0];
}
```

**Never return a reference to a local object!**. E.g.:
```c++
const string &wrong() {
    string retrn;
    if (retrn.empty())
      return retrn; // Given how the function is defined, this returns a reference to a local variable;
                    // but the local variable is discarded after the function call is processed.
                    // So the function returns a reference to an object no longer in memory
    else
      return "Wrong"; // Again, this returns a local temporary string;
}
```

#### Returning a Pointer to an array

- Using type aliases
```c++
using myArray = int[10] // Or equivalently: typedef int myArray[10];
myArray* myFunction(paramList);
```

- Not using type aliases
```c++
int (*function(paramlist))[10];
```

```c++
// Returns a dynamic memory 2D array
int** createArray(const size_t length, const size_t width) {
    int** arr = new int*[length];	// allows to create dynamic memory objects, see chapter 12
    for (int r = 0; r != length; ++r) {
        arr[r] = new int[width];
    }
    for (int r = 0; r != length; ++r) {
        for (int c = 0; c != width; ++c) {
            arr[r][c] = r*c;	// Each element is the product of the row and the column index
        }
    }
    return arr;
}

int main() {
    const size_t l = 10;
    const size_t w = 10;
    int **arr = createArray(l, w);
    for (int r = 0; r != l; ++r) {		// Prints the array
        for (int c = 0; c != w; ++c) {
            cout << setw(4) << arr[r][c];
        }
        cout << endl;
    }
}
```
- Using a trailing return type: To signal that the return follows the parameter list, we use auto where the return type ordinarily appears
```c++
auto myFunction(paramList) -> int(*)[10];
```

- Using decltype: when the arrays that the function can return are already known
```c++
int even[5] = {2, 4, 6, 8, 10};
int odd[5] = {1, 3, 5, 7, 9};
decltype(odd)* arrayPointer(bool flag) {
	return (flag)? &odd : &even;
}
```

## Overloaded Functions

Overloaded functions must differ in the number or the type(s) of their parameters. 

A parameter that has a top-level const is indistinguishable from one without a top-level const; therefore:
```c++
int sum(int a, int b); // EQUIVAlENT TO
int sum(const int a, const int b);
```
On the other hand, we can overload based on whether the parameter is a reference (or pointer) to the const or nonconst version of a given type; such consts are low-level.
```c++
int sum(int &a, int &b); // DIFFERENT FROM
int sum(const int &a, const int &b);
```
It is an error for two functions to differ only in terms of their return types.

```c++
void print(const char *cp);
void print(const int *beg, const int *end);
void print(const int ia[], size_t size);
```

```const_cast<Type &>(objectName)```: may be used to cast away (remove) constness or volatility.

## Features for Specialized Uses

### Default Arguments

If we want to use the default argument, we omit that argument when we call the function. The default arguments are used for the trailing (right-most) arguments of a call.
```c++
typedef string::size_type sz; // typedef see § 2.5.1 (p. 67)
string screen(sz ht = 24, sz wid = 80, char backgrnd = ' ');

int main {
	string str1 = screen(15, 10); // Uses ' ' as background
	string str2 = screen(15, '%'); // Cannot default the parameter wid while providing backgrnd
				       // The compiler does not yield an error, as char is impicitly converted to size_t
}
```

Although it is normal practice to declare a function once inside a header, it is legal to redeclare a function multiple times. However, each parameter can have its default specified only once in a given scope. Thus, any subsequent declaration can add a default only for a parameter that has not previously had a default specified.

### Inline and constexpr functions

**Inline Functions**: allow to avoid function call overhead. It is used to optimize small functions.
```c++
inline const string &shorterString(const string &s1, const string &s2) { 
	return s1.size() <= s2.size() ? s1 : s2;
}
```

**constexpr Functions**: functions that can be used in a constant expression. Such functions must be simple enough that the compiler
can evaluate them at compile time. We can use constexpr functions in the initializer of a constexpr variable.

**Inline and constexpr functions normally are defined in headers**

### Aids for debugging

**assert**

`assert` is a preprocessor contained in the library `<cassert>`, takes single expression and uses it as condition.  If the condition is false,  terminates the program. The behavior of assert depends on the status of a preprocessor variable named NDEBUG. If NDEBUG is defined, assert does nothing. By default, NDEBUG is not defined, so, by default, assert performs a run-time check. Use `#define NDEBUG` to define it. 

Names that can be used in debugging:
- FILE
- LINE
- TIME
- DATE

## Pointers to Functions

```c++
// compares lengths of two strings
bool lengthCompare(const string &, const string &);
// pf points to a function returning bool that takes two const string references
bool (*pf)(const string &, const string &);
pf = lengthCompare; // pf now points to the function named lengthCompare
pf = &lengthCompare; // equivalent assignment: address-of operator is optional
```

[Uses of function pointers](https://stackoverflow.com/questions/2592137/what-is-the-point-of-function-pointers)
