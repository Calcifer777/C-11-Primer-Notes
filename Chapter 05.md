# Statements

## Simple and compound statements

**Simple statements**
* *Expression statement*: expression followed by a `;`. The expression is evaluated and the result discarded. 
* *Null statement*: useful where the language requires a statement but the program’s logic does not.

**Compound Statements (blocks)**: a sequence of statements surrounded by a pair of curly braces Variables defined in the control structure are visible only within that statement. and are out of scope after the statement ends.

## Conditional statements

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

## Iterative statements

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

## Jump statements
















