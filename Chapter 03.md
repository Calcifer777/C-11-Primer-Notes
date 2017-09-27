# Chapter 3. Strings, Vectors, and Arrays

To use the `string` type:
```c++
#include <string>
using std::string;
```

## 3.1 Namespace `using` Declarations

```c++
using namespace std;
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
| `string s3 = "value"`	| `s3` is a copy of the string literal		|
| `string s3("value")`	| `s3` is a copy of the string literal		|
| `string s4(n, 'c')`	| `s4` results in `c` repeated `n` times		|

The `string` default initialization value is the **empty string**.

Using `=` **copy initializes** the string. Using brackets uses **direct initialization**.

### Operations on `string` variables

| Code				| Result 					|
| ----------------- | ------------------------- |
| `os << s` 		| Writes `s` in the output 	|
| `is >> s`			| Reads the string `si` from the input as saves it as `s`. <br /> When reading strings from input lines, `cin` reads until the first whitespace;	|
| `getline(is, s)`	| Reads a line of input from `is` into `s`	|
| `s.empty()` 		| TRUE is `s` is empty		|
| `s.size()` 		| Returns the number of characters in `s`in a `string::size_type` value	|
| `s[n]` 			| Returns the `n`th *char* in `s`			|
| `s1+s2` 			| Concatenates `s1` and `s2` or  a `string` and a literal. <br /> When using `+` in an initialization of a string at least one of the two operands has to be a string.|
| `s1=s2` 			| Replaces the value in `s1` with that `s2` |
| `s1==s2` 			| TRUE if `s1` and `s2` hold the same values|
| `s1!=s2` 			| TRUE if `s1` and `s2` hold different values |
| `<, <=, >, >=` 	| Comparisons are case sensitive and use dictionary order	|

When reading strings from input lines, `cin` reads until the first whitespace;

### Characters in strings

The functions below are defined in the `cctype` header.

| Code 				| Result						|
| ----------------- | ----------------------------- |
| `isalphanum(c)`	| TRUE if `c` is a letter or digit						|
| `isalpha(c)`		| TRUE if `c` is a letter								|
| `iscntrl(c)`		| TRUE if `c` is a control character 					|
| `isdigit(c)`		| TRUE if `c` is a digit								|
| `isgraph(c)`		| TRUE if `c` is not a space but  is printable			|
| `islower(c)` 		| TRUE if `c` is lowercase								|
| `isupper(c)` 		| TRUE if `c` is uppercase								|
| `isprint(c)`		| TRUE if c is a printable character 					|
| `ispunct(c)` 		| TRUE if `c` is a punctuation character 				|
| `isspace(c)`		| TRUE if `c` is a whitespace (\s, \n, \t, \r, \f, \v)	|
| `isxdigit(c)` 	| TRUE if `c` a hexadecimal digit 						|
| `tolower(c)` 		| Returns the lowercase equivalent of a character		|
| `toupper(c)` 		| Returns the uppercase equivalent of a character		|

### `Rangefor` 

```c++
for (declaration : expression) {
	statement
}
```

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
| `vector<T>v1`						| **v1** of type T 							|
| `vector<T>v2(v1)`					| **v2** copy of *v1* 						|
| `vector<T>v2 = v1`				| **v2** copy of *v1*							|
| `vector<T>v3(n, val)`				| **v3** is made of *val* repeated *n* times	|
| `vector<T>v4(n)`					| **v4** holds *n* initialized objects			|
| `vector<T>v5{a, b, c, ...}`		| **v5** hlds *a*, *b*, *c*, ...				|
| `vector<T>v5 = {a, b, c, ...}`	| **v5** hlds *a*, *b*, *c*, ...				|

If the vector holds elements of a built-in type, then the element initializer has a value of 0. If it holds a class type, the element initializer is itself default initialized.

### Vector operations

| Code 				| Result 				|
| ----------------- 		| --------------------------------- 	|
| `v.empty()`			| TRUE if *v* is empty 			|
| `v.size()`			| Returns the size of v 		|
| `v.push_back(obj)`		| Appends to v 				|
| `v[n]`			| Returns the nth element of v 		|
| `v1 = v2`			| **v1** is now equal to *v2* 		|
| `v1 = {a, b, ...}`		| **v1** is now *{a,b, ...}*		|
| `v1 == v2`			| TRUE if **v1** and *v2* are equal 	|
| <, <=, >, >=			| Uses dictionary order			|
| `++v[n]`			| Increments the value of the nth index |

## 3.4 Introducind Iterators

| Code 				| Result 				|
| ----------------- 		| --------------------------------- 	|
| `*iter`			| Returns a reference to the element denoted by the iterator iter 			|
| `iter->mem`			| Dereferences `iter` and fetches the member named mem from the underlying element; equivalent to `{+iter}.menu` |
| `++iter`, `--iter`		| Increments/decrements `iter` to refer to the next/previous element in the container 				|
| `iter1 == iter2`		| Compares two iterators for equality, i.e. whether they denote the same element  or if they are the off-the-end iterator for the same container	|
| `iter1 != iter2`		| Compares two iterators for inequality 		|
| `iter.begin()`		| Denotes the first element in iter |
| `iter.end()`			| DEnotes one past the last last element in `iter`|; the iterator returned is referred to as the **off-the-end-operator** |

**Iterator Types**

| Code				| Result 			|
| ----------------------------- | ----------------------------- |
| `vector<int>::iterator it;` 	| Can r/w `vector<int>` elements	|
| `string::iterator it2`	| Can r/w characters in a string	|
| `vector<int>::const_iterator`	| Can r but not w elements		|
| `string::constr_iterator it4`	| Can read but not w elements		|

If the object is `const`, then `.begin` and `.end` return a `const_iterator`; if the object is not `const`, they return `iterator`.

As do the `begin` and `end` members, these members return iterators to the first and one past the last element in the container. However, regardless of whether the vector (or string) is `const`, they return a `const_iterator`.

`(*it).empty()` \\ dereferences the iterator `it` and calls the member *empty* on the resulting object.. This Command is equivalent to the `->` operator.

**Important** Loops that use iterators should not add elements to the container to which the iterators refer.

**Operations supported by `vector` and `string` operators**

| Code				| Result 			|
| ----------------------------- | ----------------------------- |
| `iter + n`, `iter - n` 	| Returns an **operator** `n` elements forward/backward within the container |	|
| `iter += n`, `iter -= n`	| Assigns to `iter` the value of adding/subtracting `n` from/to `iter` |	|
| `iter1-iter2`	| Returns the number of places from `iter1` to `iter2`. The result type is a signed integral type named
`difference_type`	|
| `<`, `<=`, `>`, `>=`	| One operator is less than another if it appears in the container before the one referred to by the other iterator		|

## 3.5 Arrays

Like a vector, an array is a container of unnamed objects of a single type that we access by
position. **Unlike a vector, arrays have fixed size**.

If the array declarator has the form `a[d]`, where `a` is the name being defined and `d` is the dimension of the array. The
dimension specifies the number of elements and must be greater than zero. The number of elements in an array is part of the array’s type. As a result, the dimension must be known at compile time, which means that the dimension must
be a constant expression (**`constexpr`**).

Arrays can also be list initialized, in which case we need not to declare the dimension.

As with variables of built-in type, a default-initialized array of built-in type that is defined inside a function will have undefined values.

**Character arrays** can be initialized from string literals.

``` c++
	int (*pointerToArray)[10] = &arr;
	// pointerToArray points to an array of 10 ints
	
	int *(&arrRef)[10] = arr;
	// arrRef is a reference to an int array (arr) of size 10
```

When using a variable to subscript an array, that subscript should have type `size_t`.

### Pointers and array

* When using an array as the target of a pointer, the compiler substitutes a pointer to the first elelemt.

``` c++
string *p2 = nums; // equivalent to p2 = &nums[0]
```

* When using an array as an initializer for a variable using `auto` (E.g. `auto ia(arr);`) the deduced type is a pointer , not an array.
In this case, `ia` points to the first element in `arr`. This implicit conversion does not happen when using `decltype`. E.g. `decltype(arr) ia = {0, 1, 2, 3}` creates an array of 4 `int`.

Pointers to array elements support the same operations as iterators on vectors and strings.

**Example of iterator methods applied to arrays**
``` c++
	int ia[] = {0, 1, 2, 3};
	int *pbeg = begin(ia);
	int *pend = end(ia);
	
	while (pbeg != pend && *pbeg >=0) {
		cout << *pbeg;
		pbeg++;
	}
```

It is possible to initialize a vector from an array. E.g.
```c++
int int_arr[] = {0, 1, 2, 3, 4, 5};
// ivec has six elements; each is a copy of the corresponding element in int_arr
vector<int> ivec(begin(int_arr), end(int_arr));
```

**Advice: Use Library Types Instead of Arrays**

### Multidimensional Arrays ###

Multidimensional arrays are defined as:

```c++
int ia[2][3] = {
{1, 2, 3},
{4, 5, 6}};
// ia is an array of ints of 2 arrays of 3 elements each
```
Use of the for range loop with md arrays:

```c++
// print the value of each element in ia, with each inner array on its own line
// p points to an array of four ints
for (auto p = ia; p != ia + 3; ++p) {
// q points to the first element of an array of four ints; that is, q points to an int
for (auto q = p; q != p + 4; ++q)
cout << *q << ' ';
cout << endl;
}
```

**Care for the difference and handling of C-style stirngs!**










