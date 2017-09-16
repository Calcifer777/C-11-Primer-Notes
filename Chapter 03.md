# Chapter 3. Strings, Vectors, and Arrays

To use the `string` type:
```c++
#include <string>
using std::string;
```

## 3.1 Namespace `using` Declarations

```c++
using std;
```

```c++
using std::cout;
using std::cin;
```

A separate `using` declarations is required for each namespace member. 

## 3.2 Library `string` Type

### Types of `string` initialization

| Code					| Result					|
| --------------------- | ------------------------- |
| `string s1`			| Default initialization; `s1` is empty	|
| `string s2(s1)`		| `s2` is a copy of `s1`	|
| `string s1 = s2`	 	| `s2` is a copy of `s1`	|
| `string s3 = "value"	| s3 is a copy of the string literal		|
| `string s3("value")	| s3 is a copy of the string literal		|
| `string s4(n, 'c')	| s4 results in `c` repeated `n` times		|

The `string` default initialization value is the **empty string**.

Using *=* copy initializes the string. Using brackets uses *direct initialization*.

### Operations on `string` variables

| Code				| Result 					|
| ----------------- | ------------------------- |
| `os << s` 		| Writes `s` in the output 	|
| `is >> s`			| Reads the string `si` from the input as saves it as `s`; When reading strings from input lines, `cin` reads until the first whitespace;	|
| `getline(is, s)`	| Reads a line of input from `is` into `s`	|
| `s.empty()` 		| TRUE is `s` is empty		|
| `s.size()` 		| Returns the number of characters in `s`in a `string::size_type` value	|
| `s[n]` 			| Returns the `n`th *char* in `s`			|
| `s1+s2` 			| Concatenates `s1` and `s2` or  a `string` and a literal. When using `+` in an initialization of a string at least one of the two operands has to be a string.|
| `s1=s2` 			| Replaces the value in `s1` with that `s2` |
| `s1==s2` 			| TRUE if `s1` and `s2` hold the same values|
| `s1!=s2` 			| TRUE if `s1` and `s2` hold different values |
| `<, <=, >, >=` 	| Comparisons are case sensitive and use dictionary order	|

When reading strings from input lines, `cin` reads until the first whitespace;

### Characters in strings

The functions below are defined in the `cctype` header.

| Code 				| Result						|
| ----------------- | ----------------------------- |
| isalphanum(c)		| TRUE if `c` is a letter or digit						|
| isalpha(c)		| TRUE if `c` is a letter								|
| iscntrl(c)		| TRUE if `c` is a control character 					|
| isdigit(c)		| TRUE if `c` is a digit								|
| isgraph(c)		| TRUE if `c` is not a space but  is printable			|
| islower(c) 		| TRUE if `c` is lowercase								|
| isupper(c) 		| TRUE if `c` is uppercase								|
| isprint(c)		| TRUE if c is a printable character 					|
| ispunct(c) 		| TRUE if `c` is a punctuation character 				|
| isspace(c)		| TRUE if `c` is a whitespace (\s, \n, \t, \r, \f, \v)	|
| isxdigit(c) 		| TRUE if `c` a hexadecimal digit 					|
| tolower(c) 		| Returns the lowercase equivalent of a character		|
| toupper(c) 		| Returns the uppercase equivalent of a character		|

### `Rangefor` 

`for (declaration : expression)
statement`

Example

```c++
string s("Some random String");
for (auto $c : s) {				// c is a reference
	c = toupper(c);
}
```

### The subscript operator `[ ]`

Subscripts start at 0. The result of using an index outside this range is undefined; by implication, subscripting an empty string is undefined.

## 3.3 Library `vector` Template

```c++
#include <vector>
```

### Vector initialization

| Code 								| Result 									|
| --------------------------------- | ----------------------------------------- |
| `vector<T>v1`						| *v1* of type T 							|
| `vector<T>v2(v1)`					| *v2* copy of *v1* 						|
| `vector<T>v2 = v1`				| *v2* copy of *v1*							|
| `vector<T>v3(n, val)`				| *v3* is made of *val* repeated *n* times	|
| `vector<T>v4(n)`					| *v4* holds *n* initialized objects			|
| `vector<T>v5{a, b, c, ...}`		| *v5* hlds *a*, *b*, *c*, ...				|
| `vector<T>v5 = {a, b, c, ...}`	| *v5* hlds *a*, *b*, *c*, ...				|

If the vector holds elements of a built-in type, then the element initializer has a value of 0. If it holds a class type, the element initializer is itself default initialized.

### Vector operations

| Code 				| Result 							|
| ----------------- | --------------------------------- |
| `v.empty()`		| TRUE if *v* is empty 				|
| `v.size()`		| Returns the size of v 			|
| `v.push_back(obj)`| Appends to v 						|
| `v[n]`			| Returns the nth element of v 		|
| `v1 = v2`			| *v1* is now equal to *v2* 		|
| `v1 = {a, b, ...}`| *v1* is now *{a,b, ...}*			|
| `v1 == v2`		| TRUE if *v1* and *v2* are equal 	|
| <, <=, >, >=		| Uses dictionary order				|
| `++v[n]`			| Increments the value of the nth index |

## 3.4 Introducind Iterators

## 3.5 Arrays

## 3.6 Multidimensional Arrays
