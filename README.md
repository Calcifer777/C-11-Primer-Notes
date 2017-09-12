# Chapter 2 - Variables and Basic Types
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
| `long`		| 32 bits		|
| `long long`	| 64 bits		|
| `float`		| 6 sig. dig	|
| `double`		| 10 sig. dig	|
| `long double`	| 10 sig. dig	|

An `int` type will be at least as large as `short`; a `long` at least as large as an `int` and so forth.

The types `int`, `short`, `long` and `long long` are signed; add `unsigned` in the declaration command. 

The `unsigned char` type holds values from 0 to 255. `signed char` holds values rom -128 to 127.

#### Type Conversion

* Assigning a non-`bool` arithmetic type to a `bool` object, the result is false iff the value is 0; otherwise 1. Viceversa, the result is 1 if true, 0 if false.
* Assigning a floating-point value to an integer type truncates the decimal part. Viceversa, the decimal part is set to 0.
* Assigning an out-of-range value to an unsigned type returns remainder of the value modulo the number of values the target type can hold; the value "wraps around" the type ranges.
* Assigning an out-of-range value to a signed type returns undefined (the program might work or crash or produce "wrong" values). Program that use implementation-defined behavior are called *nonportable*.


In expression that mix signed and unsigned values, the signed values are automatically converted to unsigned.

##### Literals

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

## 2.3 Compound Types

## 2.4 'const' Qualifier

## 2.5 Dealing with Types

## 2.6 Defining Our Own Data Structures
