# Statements

## Simple and Compound Statements

**Simple statements**
* *Expression statement*: expression followed by a `;`. The expression is evaluated and the result discarded. 
* *Null statement*: useful where the language requires a statement but the program’s logic does not.

**Compound Statements (blocks)**: a sequence of statements surrounded by a pair of curly braces Variables defined in the control structure are visible only within that statement. and are out of scope after the statement ends.

## Conditional Statements

**`If`**

```c++
if (cond) {
	statement
} else if {
	statement 
} else {
	statement
}
```

*Dangling else*: Colloquial term used to refer to the problem of how to process nested if statements in which there are more ifs than elses. In C++, an else is
always paired with the closest preceding unmatched `if`. Note that curly braces can be used to effectively hide an inner if so that the programmer can control
which if a given else should match.

**`switch`**

```c++
switch (variable) {
	case intConstExpr1: 	// Case label: the value must be an integral constant expression
		statement1;
		break;
	...
	case intConstExprN:
		statement;
		break;
	default:
		statement;
		break;
	}
```

If a variable needs to be declared inside a switch statement AND for a particulare *case*, it is necessary define it inside a block.

## Iterative Statements

**`while`**

```c++
while (cond) {
    statement
}
```

**`do while`**

do { 
    statement
} while (*condition*);      // Remember the ";" !!!

Diffently from the `while` statement, it ensures that the loop is executed at least once.

It is not possible to define variables inside the *condition*.

**`for`**

```c++
for(*initializer*; *condition*; *expression*) {
    statement
}
```

It is possible to initialize multiple variables within the same `for` statement.

It is possible to omit any among the *init-statement*, *condition* and/or *expression* with a null statement.

**Range `for`**

for (*declaration* : *expression*) {
    statement
}

*expression* must represent a sequence or a container.

*declaration* defines a variable, such that it is  possible to convert any element of the expression sequence to the avariable `type`.

It not possible to add/remove elements to a container through  a range `for` statement.

## Jump Statements

**`break`**

A break statement terminates the nearest enclosing `while`, `do while`, `for`, or `switch` statement. Execution resumes at the statement immediately following the terminated statement.

A break can appear only within an iteration statement or switch statement (including inside statements or blocks nested inside such loops).

A break affects only the nearest enclosing loop or switch:

**`continue`**

A continue statement terminates the current iteration of the nearest enclosing loop and immediately begins the next iteration. 

A continue can appear only inside a `for`, `while`, or `do while` loop, including inside statements or blocks nested inside
such loops.

Like the break statement, a continue inside a nested loop affects only the nearest enclosing loop.

Unlike a break, a continue may appear inside a switch only if that switch is embedded inside an iterative statement.

**`goto` (DO NOT USE IT)**

A goto statement provides an unconditional jump from the goto to a another statement in the same function.

**labeled statement**: any statement that is preceded by an identifier followed by a colon.

```c++

goto end;	// Jumps to the statement labelled "end"

end : return; 	// "end" is the label for this statement
```

A jump backward over an already executed definition is okay. Jumping back to a
point before a variable is defined destroys the variable and constructs it again

## `try` Blocks and Exception Handling

Exception handling supports this cooperation between the detecting and handling parts of a program. In C++, exception handling involves
* **`throw` expressions**, which the detecting part uses to indicate that it encountered something it can’t handle. We say that a *throw* raises an *exception*.
* **`try` blocks**, which the handling part uses to deal with an exception. A `try` block starts with the keyword try and ends with one or more `catch` clauses. Exceptions thrown from code executed inside a `try` block are usually handled by one of the `catch` clauses. Because they “handle” the exception, catch clauses are also known as *exception handlers*.
• A set of *exception classes* that are used to pass information about what happened between a throw and an associated catch.

**`throw`**

```c++
throw runtime_error("Error description");
```

**`try` blocks**

```c++ 
try {
	program-statements
} catch (exception-declaration) {
	handler-statements
} catch (exceltion-declaration) {
	handler-statements
} // ...
```

### Standard Exceptions

Headers that contain exception classes:
* **`exception`**: defines the most general kind of exception class named `exception`. It communicates only that an exception occurred but provides no additional information.
* **`stdexcept`**: defines several hgeneral-purpouse exception classes, as listed below.

| Code 					| Description																	|
| --------------------- | ----------------------------------------------------------------------------- |
| `exception`			| General exception																|
| `runtime_error`		| Problem that can be detected only at runtime (RTE)							|
| `range_error`			| RTE: result generated outside the range of values that are meaningful			|
| `overflow_error`		| RTE: computation that overflowed												|
| `underflow_error`		| RTE: computation that underflowed												|
| `logic_error`			| Error in the logic of the program (L)											|
| `domain_error`		| LE: argument for which no result exists										|
| `invalid_argument`	| LE: inappropriate argument													|
| `length_error`		| LE: attempt to create an object larger thatn the maximum size for that type	|
| `out_of_range`		| LE: used a value ouside the valid range										|


* **`new`**: defines the `bad_alloc` exception type.
* **`type_info`**: defines the `bad_cast` exception type.
