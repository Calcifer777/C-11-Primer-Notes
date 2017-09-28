
# Expressions

## Intro

A **unary operator** acts on one operand; a **binary operator** acts on two.

**Operand conversions**: implicit conversion that operands undergo when evaluated within an expression. 

**Oveloaded operator** is a built in operator that can be applied to class types; in such cases the meaning and the application of that operator may change. However the number of operands, the precedence and associativity of the operand cannot be changed.

**Precedence**: the order in which different operands are evaluated within an expression.

**Associativity (Left or right)** The order in which concatenated instances of the same operand are evaluated.

IO operators are left associative.

Assignment is right associative AND has low precendence.

The order of evaluation of the operands in an expression is independent from the precedence of the oretators within the expression.

### Rvalues and Lvalues

Roughly speaking, when we use an object as an rvalue, we use the object’s value (its contents). When we use an object as an
lvalue, we use the object’s identity (its location in memory).

An lvalue expression yields an object of a function; however it may not be the left-hand operand of an assignment
  
It is possible to use an lvalue when a rvalue is required, but not viceversa.

Lvalues and rvalues also differ when used with `decltype`. When we apply decltype to an expression (other than a variable), the result is a reference type if the expression yields an lvalue. As an example, assume `p` is an `int*`. Because dereference yields an lvalue, `decltype(*p)` is `int&`. On the other hand, because the address-of operator yields an rvalue, decltype(&p) is `int**`, that is, a pointer to a pointer to type int.

## Classes of operators

### Increment and decrement operators 

**Prefix operator** `++i`

**Postfix operator** `i++`

### Member access operator

The dot and arrow operators provide for member access. The dot operator fetches a member from an object of class type; arrow is
defined so that `ptr->mem` is a synonym for `(*ptr).mem`.

``` c++
  string s1 = "Hello";
  string * ptr = &s1;
  auto n = s1.size();
  n = (*ptr).size();
  n = ptr -> size();
    \\ The 3 statements above are equivalent
```

### Conditional operator

`(cond ? ) expr1 : expr2;`

### Bitwise operators

* AND:        `&`
* OR:         `|`
* Not:        `~`
* XOR:        `^`
* Left Shift: `<<`
* Right Shift:`>>`

### Sizeof operator

Returns the size, in bytes, of an expression or a type name.

Examples:
* `sizeof (int)`        Returns the size of an int object
* `sizeof myClass`      Returns the size of a `myClass` oobject
* `sizeof ptr`          Returns the size of a pointer
* `sizeof *ptr`         Returns the size of the object to which ptr points
* sizeof a string or a vector returns only the size of the fixed part of these types; it does not return the size used by the object’s elements
* `sizeof arr`          Returns the size of the entire array. `sizeof arr` divided by the size of the elements yields the number of elements in the array.

### Comma operator

The comma operator takes two operands, which it evaluates from left to right.
Like the logical AND and logical OR and the conditional operator, the comma
operator guarantees the order in which its operands are evaluated.

## Type conversions

### Implicit conversions

The compiler automatically converts operands in the following circumstances:
* Arithmetic conversions: n arithmetic and relational expressions with operands of mixed types, the
types are converted to a common type.
  * **Integral promotions**: In most expressions, values of integral types smaller than int are first promoted to an appropriate larger     integral type.
  * If the operands of an operator have differing types, those operands are ordinarily converted to a common type. If any operand is an unsigned type, the type to which the operands are converted depends on the relative sizes of the integral types on
    the machine.
* In conditions, nonbool expressions are converted to bool.
* In initializations, the initializer is converted to the type of the variable; in
  assignments, the right-hand operand is converted to the type of the lefthand.

### Explicit conversions

** Static Cast **
`type var = static-name<type> (expression)`

** Const Cast **
`const_cast<type>` 
Can cast "away" the const, so that the object can be rewritten. `const_cast` only changes constness

** Reinterpret Cast **
Generally performs a low-level reinterpretation of the bit pattern of its operands

** Dynamic Cast**
Given a class Base of which there is a derived class Derived, dynamic_cast will convert a Base pointer to a Derived pointer if and only if the actual object pointed at is in fact a Derived object.








