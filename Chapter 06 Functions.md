# Functions

## Basics

A function can not return an array type or a function type, but it can return a pointer to array or a pointer to a function.

**Local variables** Variables defined inside a block.

**Automatic object**: an object that exists only while a block is executing. Automatic objects corresponding to local
variables are initialized if their definition contains an initializer. Otherwise, they are default initialized, which means that uninitialized local variables of built-in type have undefined values.

**Local static object**: local objects whose value persists across calls to the function. Local static objects that are created and initialized before control reaches their use and are destroyed when the program ends.

**Function declaration (prototypes)**: `returnType functionName(typeP1 p1, typeP2 p2 ...);` . The header that declares a function should be included in the source file that defines that function.

## Argument Passing

### Passing Arguments by Value

Passing an argument by value works exactly the same way; nothing the function
does to the parameter can affect the argument.

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

Using a reference instead of a reference to const limits the type of arguments that can be used with the function. We cannot pass a const object, or a literal, or an object that requires conversion to a plain reference parameter.

##### Passing arrays

If we pass an array to print, that argument is automatically converted to a pointer
to the first element in the array; the size of the array is irrelevant.

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

**Passing a Multidimensional Array**: As with any array, a multidimensional array is passed as a pointer to its first
element. Because we are dealing with an array of arrays, that element is an array, so the pointer is a pointer to an array. The size of the second (and any subsequent) dimension is part of the element type and must be specified

## Return types and the `return` Statement

## Overloaded Functions

## Features for Specialized Uses

## Function Matching

## Pointers to Functions
