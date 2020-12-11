# The Language

C is a general-purpose imperative procedural computer programming language that supports structured programming, lexical variable scope, and recursion, with a static type system.

C was originally developed at Bell Labs by Dennis Ritchie between 1972 and 1973 to construct utilities running on Unix. It was applied to re-implementing the kernel of the Unix operating system. During the 1980s, C gradually gained popularity. It has become one of the most widely used programming languages. 

C was designed to be compiled to give low-level access to memory and language constructs that map efficiently to machine instructions, all with minimal run-time support.

Because of its design, C has found lasting use in applications previously coded in assembly language. Such applications include operating systems and various application software for computer architectures that range from supercomputers to programmable logic controllers (PLC) and embedded systems.

Despite its low-level capabilities, the language was designed to encourage cross-platform programming. A C program written with portability in mind can be compiled for a wide variety of platforms and operating systems with few changes to its source code.

C has been standardised by the ANSI since 1989 (ANSI C) and by the International Organisation for Standardisation (ISO). 

As of September 2020, C is the most popular programming language.

## Its creator

Dennis MacAlistair Ritchie (September 9, 1941 – c. October 12, 2011) was an American computer scientist. He created the C programming language and, with his long-time colleague Ken Thompson, he also created the Unix operating system and B programming language. 

Ritchie and Thompson were awarded the Turing Award from the ACM in 1983, the Hamming Medal from the IEEE in 1990 and the National Medal of Technology from President Bill Clinton in 1999. 

Ritchie was the head of Lucent Technologies System Software Research Department when he retired in 2007. 

He was the "R" in K&R C, and commonly known by his username **dmr**.

## Popular Features

- **Procedural**

  C follows the procedural paradigm which is a branch of structured programming.

  In procedural programming, a program is written as a series of tasks. The tasks are carried out one after another which is basically a top to bottom order of doing things.

  A series of tasks can be wrapped inside a subroutine to form a procedure, which can be called at any point during a program's execution.

  Procedural nature of C makes writing programs in it intuitive and easy

- **Performant**

  C has the best execution speed among programming languages in use today.

  The reasons behind C's high performance are as follows:

  - It's compiled. Code written in C is converted to assembly language before execution. Since the executable is as close to the machine code as possible, fast execution is guaranteed. 
  - It's statically typed. Type of variables once declared do not change. There is no need of handling constantly changing types because of which a lot of valuable execution time is saved.
  - It has no garbage collection[^GC]. The programmer is responsible for managing the memory (allocation and de-allocation). Because of absence of automatic memory management, there is no processing overhead to degrade performance.

  C's speed makes it ideal for embedded systems and real time applications.

  [^GC]: GC is a form of automatic memory management. It attempts to reclaim garbage, or memory occupied by objects that are no longer in use by the program. 

- **Modular**

  Modularity allows a program to be broken into smaller units and run individually. 

  In C, modularity in achieved by using header files. Header files are separate files to store functions and procedures which we can pull into our code by including their header in our main program file.

  Because of C's modularity, we can use pieces of code from libraries and utilities to make our work easier. 

  Maintainability and re-usability are direct benefits of the language's modular nature.

- **Portable**

  Portable means that the same code, with slight or no changes, works on different platforms. 

  C, by design, was made to encourage cross platform programming. A program using the standard library can be compiled for a wide variety of platforms and operating systems, though programs written with platform specific libraries and commands need little changes.

- **Rich Functions Library**

  C's standard library assists us in doing most of the low level and difficult tasks like I/O, memory management, threading, date-time, error-handling and numerics. It hides all the messy details and gives us neat ready-to-use functions which we can use to quickly get our job done.

- **Rich Set of Built-In Operators**

  Many common programming operations are supported by a rich set of operators which includes arithmetic, assignment, comparison, increment / decrement, logical, bit-wise and member access operators. 

- **Statically Typed**

  Objects, functions, and expressions have a property called *type*, which determines the interpretation of the binary value stored in an object or evaluated by the expression.

  C is a statically typed language which means the types of objects, functions and expressions are checked before run time (i.e. at compile time). Static type checking ensures that no type errors occur at run time. Type errors happen when two entities of incompatible types interact. For e.g. The system doesn't know what to output when you add a number to a string `5 + 'John'`, so it shows an error.

  Static typing saves us from such undefined behaviour during execution. 

## Overview / Characteristics

- The language has a small, fixed number of keywords, including a full set of control flow primitives: `if/else`, `for`, `do/while`, `while`, and `switch`. User-defined names are not distinguished from keywords by any kind of sigil.
- It has a large number of arithmetic, bit-wise, and logic operators: `+`, `+=`, `++`, `&`, `||`, etc.
- More than one assignment may be performed in a single statement.
- Data typing is static, but weakly enforced; all data has a type, but implicit conversions are possible.
- Declaration syntax mimics usage context. C has no "define" keyword; instead, a statement beginning with the name of a type is taken as a declaration. There is no "function" keyword; instead, a function is indicated by the presence of a parenthesised argument list.
- User-defined (`typedef`) and compound types are possible.
- Heterogeneous aggregate data types (`struct`) allow related data elements to be accessed and assigned as a unit.
- Union is a structure with overlapping members; only the last member stored is valid.
- Array indexing is a secondary notation, defined in terms of pointer arithmetic. Unlike structs, arrays are not first-class objects: they cannot be assigned or compared using single built-in operators. There is no "array" keyword in use or definition; instead, square brackets indicate arrays syntactically, for example `month[11]`.
- Enumerated types are possible with the `enum` keyword. They are freely inter-convertible with integers.
- Strings are not a distinct data type, but are conventionally implemented as null-terminated character arrays.
- Functions:
  - Function return values can be ignored, when not needed.
  - Function and data pointers permit *ad hoc* run-time polymorphism.
  - Functions may not be defined within the lexical scope of other functions.
- Procedures (subroutines not returning values) are a special case of function, with an un-typed return type `void`.
- Low-level access to computer memory is possible by converting machine addresses to typed pointers.
- A preprocessor performs macro definition, source code file inclusion, and conditional compilation.
- There is a basic form of modularity: files can be compiled separately and linked together, with control over which functions and data objects are visible to other files via `static` and `extern` attributes.
- Complex functionality such as [I/O](https://en.wikipedia.org/wiki/Input/output), string manipulation, and mathematical functions are consistently delegated to library routines.

While C does not include certain features found in other languages (such as object orientation and garbage collection), these can be implemented or emulated, often through the use of external libraries (e.g., the GLib Object System or the Boehm garbage collector).

<div style="page-break-after: always; break-after: page;"></div> 

## Structure of a Program

A C program is a sequence of text files (typically header and source files) that contain declarations. They undergo translation to become an executable program, which is executed when the OS calls the main function.

```c
// program.c

// DOCUMENTATION SECTION
/*
 *  Purpose : A simple program to
 *            print Hello World.
 * 
 *  Author  : Abhigyan Prakash
 *  Created : Wed Sep 23 2020 16:49:40
*/

// LINK SECTION
#include <stdio.h>

// GLOBAL DECLARATION SECTION
char* message = "Hello World";
void showMessage();

// MAIN SECTION
void main(void) {
    showMessage();
}

// USER DEFINED FUNCTIONS
void showMessage() {
    printf("%s\n", message);
}
```

A typical C program is divided into the following sections in order.

- **Documentation Section**

  In this section, we write comments about the program. We can state the purpose, creation time, modification time, author's name etc. These comments are for anyone who'll read our source code in future.

  We can use either comment type, single line `//...` or multi line `/* … */`.

  Documentation section has nothing to do with the program's execution. 

- **Link Section**

  This section is used to link code in other files (headers) with our program. We can specify the headers we want to include using the syntax `#include <headerName.h>`. Once a header is linked, we can pull the code declarations (functions, constants, types) inside them and use them in our code. 

  Link section gives us the access to many useful standard and third party libraries. 

- **Global Declaration Section**

  We can use this section to define constant values and expressions, user defined types,  global variables, structures, unions, and prototypes of user defined functions (UDFs). 

  Defining these entities here makes them available at the file scope (hoisted) which means that they will be accessible by  `main()` or any other function in the current file.

  For UDFs, this section is not limited to their declarations; we can put complete UDF definitions here as well. But in doing so we'll have to keep in mind that a UDF using another UDF must be placed after the UDF it's using.

- `main()`

  This section comprises the `main()` function definition. There can only be one main in a program.

  Execution of any C program begins from this section. Other UDFs and library functions are called from main's body depending upon the logic.

- **User Defined Functions**

  A function is a block of reusable code to do specific work. 

  While C has many inbuilt functions, a programmer may need custom or user defined functions (UDFs) for various reasons. The language allows programmers to define custom functions at the end of the program file after main's body.

  However, the UDFs defined here must have their declarations in the global declaration section otherwise there will be compiler errors.

<div style="page-break-after: always; break-after: page;"></div>

## Data-types

A data type or simply type is an attribute of data which tells the compiler or interpreter how the programmer intends to use the data. 

A data type does the following:

- It provides a set of values from which an expression (i.e. variable, function, etc.) may take its values.
- It constrains the values that an expression, such as a variable or a function, might take.
- It defines the operations that can be done on the data.
- It defines the way values of that type can be stored. 

There are only a few basic data types in C:

- `char`

  A single byte, capable of holding one character in the local character set

- `int`

  An integer, typically reflecting the natural size of integers on the host machine.

- `float`

  Single-precision floating point.

- `double`

  Double-precision floating point

In addition, there are a number of qualifiers that can be applied to these basic types.

- `short` and `long`

  These apply to integers and provide different lengths of integers where possible. E.g. `short int i;` `long int c;`

  The word `int` can be omitted in such declarations. So the above examples can be written as `short i;` `long c;`

- `signed` and `unsigned`

  These may be applied to `char` or integer.

  - `unsigned` numbers are always positive or zero, and obey the laws of arithmetic modulo 2^n^, where *n* is the number of bits in the type.
  - Plain chars may be `signed` or `unsigned`, but printable chars are always positive.

- `long double` specifies extended-precision floating point.

Here's a list of all the data types available in C.

|        DATA TYPE         | MEMORY (BYTES) |              RANGE              | FORMAT SPECIFIER |
| :----------------------: | :------------: | :-----------------------------: | :--------------: |
|          `char`          |       1        |           -128 to 127           |       `%c`       |
|     `unsigned char`      |       1        |            0 to 255             |       `%c`       |
|       `short int`        |       2        |        -32,768 to 32,767        |      `%hd`       |
|   `unsigned short int`   |       2        |           0 to 65,535           |      `%hu`       |
|          `int`           |       4        | -2,147,483,648 to 2,147,483,647 |       `%d`       |
|      `unsigned int`      |       4        |       0 to 4,294,967,295        |       `%u`       |
|        `long int`        |       8        | -2,147,483,648 to 2,147,483,647 |      `%ld`       |
|   `unsigned long int`    |       8        |       0 to 4,294,967,295        |      `%lu`       |
|     `long long int`      |       8        |       -(2^63) to (2^63)-1       |      `%lld`      |
| `unsigned long long int` |       8        | 0 to 18,446,744,073,709,551,615 |      `%llu`      |
|         `float`          |       4        |                                 |       `%f`       |
|         `double`         |       8        |                                 |      `%lf`       |
|      `long double`       |       16       |                                 |      `%Lf`       |

 <div style="page-break-after: always; break-after: page;"></div>

## Tokens

Tokens are the smallest independent units in a program.

There are seven classes of tokens: 

- identifiers
- keywords
- constants
- string literals
- operators
- statement terminator
- comments
- white spaces ( spaces, horizontal & vertical tabs, new lines, form feeds )

### Keywords

Keywords are reserved words. They are used by the language and have special meaning. 

They are not available for redefinition. We cannot use them as variable or function names.

### Identifiers

An identifier is a sequence of letters and digits used to denote one of the following types of entities:

- objects
- functions
- tags ( structs, unions or enumerations )
- structure or union members
- typedef names
- label names
- macro names
- macro parameter names

The first character of an identifier must be a letter; the underscore _ counts as a letter. Upper and lower case letters are different.

Identifiers may have any length, and for internal identifiers, at least 31 characters are significant.

#### Variable

A **variable**, or an identified object, is a location in memory that can hold values and its *type* determines the meaning of the value inside it. 

A variable has a *storage class* and *scope*; storage class specifies the variable's lifetime and scope is the region of the program in which it is known. It also has a linkage which determines whether the same name in another scope refers to the same object or function.

#### Scope of a Variable

Scope refers to what parts of the program can “see” a declared variable. A declared variable can be visible only within a particular function, or within a particular file, or may be visible to an entire set of files by way of including header files and using `extern` declarations.

C has the following kinds of scopes:

##### Global (File Scope)

Global declarations are declarations made at the top-level of a file (i.e., not within a function). Their scope begins at the point of declaration and ends at the end of the file. They are visible to the entire file, including from within functions, but are not visible outside of the file.

```c
int i; // scope of i begins

// scope of g begins (note, "a" has block scope)
static int g(int a) { return a; }

int main(void)
{
    i = g(2); // i and g are in scope
}
```

##### Local

Variable declarations made within functions, function prototypes or blocks have local scope, meaning that they are visible only within the respective entity in which they have been declared.

- **Block Scope**

  The scope of any variable or identifier declared inside a compound statement, including function bodies, or in any expression, declaration, or statement appearing in if, switch, for, while, or do-while statement, or within the parameter list of a function definition begins at the point of declaration and ends at the end of the block or statement in which it was declared.

- **Function Scope**

  The scope of any variable or identifier declared within the parameter list of a function definition begins and ends with the block of the function definition.

  ```c
  void f(int n) // scope of the function parameter 'n' begins
  { // the body of the function begins
     
     ++n; // 'n' is in scope and refers to the function parameter
     
     for(int n = 0; n<10; ++n) { // scope of loop-local 'n' begins
         printf("%d\n", n); // prints 0 1 2 3 4 5 6 7 8 9
     } // scope of the loop-local 'n' ends
     
     // the function parameter 'n' is back in scope
     printf("%d\n", n); // prints the value of the parameter
     
  } // scope of function parameter 'n' ends
  
  int a = n; // Error: name 'n' is not in scope
  ```

- **Function Prototype Scope**

  The scope of a name introduced in the parameter list of a function prototype (declaration that is not a definition) ends at the end of the function prototype declarator.

  ```c
  int f(int n,
        int a[n]); // n is in scope and refers to the first parameter
  ```

#### Storage class specifier

There are four storage class specifiers that you can prepend to your variable declarations which change how the variables are stored in memory: `auto`, `extern`, `register`, and `static`.

- `auto`

  You use `auto` for variables which are local to a function, and whose values should be discarded upon return from the function in which they are declared. This is the default behavior for variables declared within functions.

  ```c
  void foo (int value) {
    auto int x = value;
    // …
    return;
  }
  ```

- `extern`

  `extern` is useful for declaring variables that you want to be visible to all source files that are linked into your project. You cannot initialise a variable in an `extern` declaration, as no space is actually allocated during the declaration. You must make both an `extern` declaration (typically in a header file that is included by the other source files which need to access the variable) and a non-`extern` declaration which is where space is actually allocated to store the variable. The `extern` declaration may be repeated multiple times.

  ```c
  extern int numberOfClients;
  …
  int numberOfClients = 0;
  ```

- `static`

  `static` is essentially the opposite of `auto`: when applied to variables within a function or block, these variables will retain their value even when the function or block is finished. This is known as *static storage duration*.

  ```c
  #include <stdio.h>
  
  int* f() { 
    static int n = 20;
    return &n; 
  }
  
  void main() {
    int *ptr_to_that_n = f();
    printf("%d\n", *ptr_to_that_n); // -> 20
  }
  ```

- `register`

  `register` is nearly identical in purpose to `auto`, except that it also suggests to the compiler that the variable will be heavily used, and, if possible, should be stored in a register. You cannot use the address-of operator to obtain the address of a variable declared with `register`. This means that you cannot refer to the elements of an array declared with storage class `register`. In fact the only thing you can do with such an array is measure its size with `sizeof`. GCC normally makes good choices about which values to hold in registers, and so `register` is not often used.

#### Lifetime (storage duration) of a Variable

The lifetime of a variable or object is the time period in which the variable/object has valid memory. It can be of the following three types:

- **Static**

  Lifetime of a static variable is the entire duration of the program's execution.

  Static variables are stored in the data segment of the "object file" of a program.

- **Automatic**

  An automatic variable has a lifetime that begins when program execution enters the function or statement block or compound and ends when execution leaves the block. 

  Automatic variables are stored in a "function call stack".

- **Dynamic** 

  The lifetime of a dynamic object begins when memory is allocated for the object (e.g., by a call to `malloc()` or using `new`) and ends when memory is de-allocated (e.g., by a call to `free()`). 

  Dynamic objects are stored in "the heap".

### Constants

Constants are fixed values that a program can't alter during execution.

There are several types of constants:

#### Integer Constant

An integer constant is a sequence of digits. 

It can be represented either in octal, decimal or hexadecimal.

| representation | begins with | example                       |
| -------------- | ----------- | ----------------------------- |
| decimal        | `1 - 9`     | `36`                          |
| octal          | `0`         | `012` `( 10 in decimal )`     |
| hexadecimal    | `0x`        | `0xAB0` `( 2736 in decimal )` |

It may have suffixes to denote value types.

| suffix     | type          |
| ---------- | ------------- |
| `u` or `U` | unsigned      |
| `l` or `L` | long          |
| `UL`       | unsigned long |

#### Character Constant

A character constant can be either a single character enclosed in quotes as in  'x', or an integer value representing a character in the machine's character set.

##### Escape Sequence

Not all characters can be expressed simply. For instance, if we want to use the non-printable ones and the ones being used by the language as special symbols, we'll have to use the corresponding escape sequences. 

An escape sequence is a series of characters prefixed with a back slash `\`.  This sequence acts like a single character.

The back slash `\` is considered an 'escape' character as it causes an escape from the normal interpretation of a string, so that the next character is recognised as one having a special meaning.



| name            | character | escape character |
| --------------- | --------- | ---------------- |
| newline         | `NL`      | `\n`             |
| horizontal tab  | `HT`      | `\t`             |
| vertical tab    | `VT`      | `\v`             |
| backspace       | `BS`      | `\b`             |
| carriage return | `CR`      | `\r`             |
| form feed       | `FF`      | `\f`             |
| audible alert   | `BEL`     | `\a`             |
| backslash       | `\`       | `\\`             |
| question mark   | `?`       | `\?`             |
| single quote    | `'`       | `\'`             |
| double quote    | `"`       | `\"`             |
| octal number    | `ooo`     | `\ooo`           |
| hex number      | `hh`      | `\xhh`           |

#### Floating Constant

A floating constant is a number that consists of an integer part, a decimal point, a fraction part, an `e` or `E` with an optionally signed integer exponent and an optional type suffix, one of `f`, `F`, `l`, or `L`.

- The integer and fraction parts both consist of a sequence of digits.

- Either the integer part, or the fraction part (not both) may be missing.

- Either the decimal point or the `e` and the exponent (not both) may be missing.

- The type of value is determined by the suffix:

  | Suffix     | Type          |
  | ---------- | ------------- |
  | `F` of `f` | `float`       |
  | no suffix  | `double`      |
  | `l` or `L` | `long double` |

#### Enumeration Constant

Identifiers declared as enumerators are constants of type `int`.

### String Literals

A string literal, also called a string constant, is a sequence of characters surrounded by double quotes as in `"apples"`.

It has type 'array of characters' and storage class `static` and is initialised with the given characters.

Strings have a null  byte `\0` as their last character to denote the end.

String literals do not contain newline or quote characters. So, to represent them, the same escape sequence as for character constants are used.

<div style="page-break-after: always; break-after: page;"></div>

### Operators

Operators are special symbols used to do common operations on the given data.

A unary operator works on one operand, a binary operator works on two operands, a ternary operator works on three operands and so on.

##### Precedence

Operator precedence determines the grouping of terms in an expression and decides how an expression is evaluated. Certain operators have higher precedence than others; for example, the multiplication operator has a higher precedence than the addition operator.  Within an expression, higher precedence operators will be evaluated first.

For example, x = 7 + 3 * 2; here, x is assigned 13, not 20 because operator * has a higher precedence than +, so it first gets multiplied with 3*2 and then adds into 7.

Here, operators with the highest precedence appear at the top of the table, those with the lowest appear at the bottom.

|    Category    |             Operator              | Associativity |
| :------------: | :-------------------------------: | :-----------: |
|    Postfix     |         () [] -> . ++ - -         | Left to right |
|     Unary      |  + - ! ~ ++ - - (type)* & sizeof  | Right to left |
| Multiplicative |               * / %               | Left to right |
|    Additive    |                + -                | Left to right |
|     Shift      |               << >>               | Left to right |
|   Relational   |             < <= > >=             | Left to right |
|    Equality    |               == !=               | Left to right |
|  Bitwise AND   |                 &                 | Left to right |
|  Bitwise XOR   |                 ^                 | Left to right |
|   Bitwise OR   |                \|                 | Left to right |
|  Logical AND   |                &&                 | Left to right |
|   Logical OR   |               \|\|                | Left to right |
|  Conditional   |                ?:                 | Right to left |
|   Assignment   | = += -= *= /= %=>>= <<= &= ^= \|= | Right to left |
|     Comma      |                 ,                 | Left to right |

##### Associativity

The associativity of an operator is a property that determines how operators of the same precedence are grouped in the absence of parentheses.

Operators may be **associative** (meaning the operations can be grouped arbitrarily), **left-associative** (meaning the operations are grouped from the left), **right-associative** (meaning the operations are grouped from the right) or **non-associative** (meaning operations cannot be chained, often because the output type is incompatible with the input types).

#### Arithmetic

The basic arithmetic operators are `+`, `-`, `*`, `/` and `%`.

- `*`, `/`, and `%` are binary operators
- `+` and `-` are unary as well as binary
- Integer division truncates any fractional parts. The direction of truncation is machine-dependent for negative operands.
- The `%` operator cannot be applied to a float or double. Sign of the result for `%` are machine-dependent for negative operands.
- Precedence:   {`+`, `-`} binary    **<**   { `*`, `/`, `%`}   **<**   {`+`, `-`} unary
- Associativity:   Left to right.

#### Comparison

Comparison operators are binary operators that test a condition and return `1` if that condition is logically **true** and `0` if that condition is **false**.

They are of the following two types:

- Equality  {`==`, `!=`}
- Relational  {`>`, `>=`, `<`, `<=`}

| Operator | Operator name            | Example  |
| :------- | :----------------------- | :------- |
| `==`     | equal to                 | `a == b` |
| `!=`     | not equal to             | `a != b` |
| `<`      | less than                | `a < b`  |
| `>`      | greater than             | `a > b`  |
| `<=`     | less than or equal to    | `a <= b` |
| `>=`     | greater than or equal to | `a >= b` |

- Precedence:    {`==`, `!=`}    **<**    {`>`, `>=`, `<`, `<=`}; comparison operators have lower precedence than arithmetic operators.
- Associativity:    Left to right.

#### Logical

Logical operators apply standard Boolean algebra operations to their operands.

| Operator | Operator name | Example  | Result                             |
| :------- | :------------ | :------- | :--------------------------------- |
| `!`      | logical NOT   | `!a`     | the logical negation of **a**      |
| `&&`     | logical AND   | `a && b` | the logical AND of **a** and **b** |
| `||`     | logical OR    | `a || b` | the logical OR of **a** and **b**  |

- The logical NOT expression has the form `!expression`, where `expression` is of scalar type (integer or pointer). It  has type `int` and its value is `0` if expression evaluates to a value that is not equal to zero. Its value is `1` if expression evaluates to a value that is equal to zero.
- The logical AND expression has the form `lhs && rhs`, where `lhs` and `rhs` are scalar expressions. It has type `int` and the value `1` if both `lhs` and `rhs` compare unequal to zero. It has the value `0` otherwise. `rhs` is only evaluated if `lhs` is not equal to `0`.
- The logical OR expression has the form `lhs || rhs`, where `lhs` and `rhs` are scalar expressions. It has type `int` and the value `1` if either `lhs` or `rhs` is equal to zero. It has the value `0` otherwise. `rhs` is only evaluated if `lhs` is equal to `0`.

#### Increment /Decrement

Increment/decrement operators are unary operators that increase/decrease the value of a variable by 1.

They can have postfix form:

- `var++`
- `var–`

As well as the prefix form:

- `++var`
- `–var`

In both prefix and postfix forms, the effect is to increment / decrement `var`. But the prefix form increases /decreases `var`  *before* its value is used, while the postfix form increases / decreases `var` *after* its value has been used.

This means that in a context where the value is being used, not just the effect, `++var` and `var++` are different. 

For example, if `n` is `5`, then

`x = n++` sets `x` to `5`, but

`x = ++n` sets `x` to `6`.

In both cases `n` becomes `6`.

The increment and decrement operators can only be applied to variables; an expression like `(i+j)++` is illegal.

#### Member Access

Member access operators allow access to the members of their operands.

| Operator | Operator name                 | Example | Description                                                  |
| :------- | :---------------------------- | :------ | :----------------------------------------------------------- |
| `[]`     | array subscript               | `a[b]`  | access the **b**th element of array **a**                    |
| `*`      | pointer de-reference          | `*a`    | de-reference the pointer **a** to access the object or function it refers to |
| `&`      | address of                    | `&a`    | a pointer that refers to the object or function **a**        |
| `.`      | member access                 | `a.b`   | access member **b** of struct or union **a**                 |
| `->`     | member access through pointer | `a->b`  | access member **b** of struct or union pointed to by **a**   |

#### Bit-wise

Bit-wise operators are used to operate on bit level. Operations are handled bit by bit. In other words, each bit of the operand(s) is individually operated.

Even though these operators operate one bit at a time, they cannot accept anything smaller than a byte as their input.

Bitwise operations are contrasted by byte-level operations where operations are performed on strings of eight bits (known as bytes) at a time. The reason for this is that a byte is normally the smallest unit of addressable memory.

The bitwise arithmetic operator expressions have the form.

| Operator     | Operator name | Operation                                                    |
| ------------ | ------------- | ------------------------------------------------------------ |
| `~rhs`       | bitwise NOT   | Takes a number and inverts all its bits.                     |
| `lhs & rhs`  | bitwise AND   | Performs AND on every bit of the two operands. The result of AND is 1 only if both bits are 1. |
| `lhs | rhs`  | bitwise OR    | Performs OR on every bit of the two operands. The result of OR is 1 if any of the two bits is 1. |
| `lhs ^ rhs`  | bitwise XOR   | Performs XOR on every bit of the  two operands. The result of XOR is 1 if the two bits are different. |
| `lhs << rhs` | left shift    | Left shifts the bits of the first operand, the second operand decides the number of places to shift. |
| `lhs >> rhs` | right shift   | Right shifts the bits of the first operand, the second operand decides the number of places to shift. |

#### Assignment

Assignment and compound assignment operators are binary operators that modify the variable to their left using the value to their right.

The simple assignment operator expressions have the form.

`lhs = rhs`, where

`lhs`: modifiable lvalue expression of any complete object type.

`rhs`: expression of any type implicitly convertible to `lhs` or compatible with `lhs`.

| Operator | Operator name                  | Example   | Equivalent of |
| :------- | :----------------------------- | :-------- | :------------ |
| `=`      | basic assignment               | `a = b`   | N/A           |
| `+=`     | addition assignment            | `a += b`  | `a = a + b`   |
| `-=`     | subtraction assignment         | `a -= b`  | `a = a - b`   |
| `*=`     | multiplication assignment      | `a *= b`  | `a = a * b`   |
| `/=`     | division assignment            | `a /= b`  | `a = a / b`   |
| `%=`     | modulo assignment              | `a %= b`  | `a = a % b`   |
| `&=`     | bitwise AND assignment         | `a &= b`  | `a = a & b`   |
| `|=`     | bitwise OR assignment          | `a |= b`  | `a = a | b`   |
| `^=`     | bitwise XOR assignment         | `a ^= b`  | `a = a ^ b`   |
| `<<=`    | bitwise left shift assignment  | `a <<= b` | `a = a << b`  |
| `>>=`    | bitwise right shift assignment | `a >>= b` | `a = a >> b`  |

Precedence:    Lowest

#### Others

A collection of operators that do not fit into any of the other major categories.

| Operator               | Operator name        | Example          | Description                                                  |
| :--------------------- | :------------------- | :--------------- | :----------------------------------------------------------- |
| `(...)`                | function call        | `f(...)`         | call the function **f**(), with zero or more arguments       |
| `,`                    | comma operator       | `a, b`           | evaluate expression **a**, disregard its return value and complete any side-effects, then evaluate expression **b**, returning the type and the result of this evaluation |
| `(type)`               | type cast            | `(type)a`        | cast the type of **a** to **type**                           |
| `? :`                  | conditional operator | `a ? b : c`      | if **a** is logically true (does not evaluate to zero) then evaluate expression **b**, otherwise evaluate expression **c** |
| `sizeof`               | `sizeof`operator     | `sizeof a`       | the size in bytes of **a**                                   |
| `_Alignof` (since C11) | `_Alignof` operator  | `_Alignof(type)` | the alignment required of **type**                           |

### Statement Terminator

A semicolon is used to mark the end of a statement and hence it is called the statement terminator.

`statement1;`

`statement2;`

### Comments

Comments serve as a sort of in-code documentation. When inserted into a program, they are effectively ignored by the compiler; they are solely intended to be used as notes by the humans that read source code.

We have the following two types of comments.

- `/* comment */`

  Often known as "C-style" or "multi-line" comments.

  C-style comments are usually used to comment large blocks of text or small fragments of code; however, they can be used to comment single lines. To insert text as a C-style comment, simply surround the text with `/*` and `*/`. C-style comments tell the compiler to ignore all content between `/*` and `*/`. 

- `// comment`

  Often known as "C++-style" or "single-line" comments.

  C++-style comments are usually used to comment single lines of text or code; however, they can be placed together to form multi-line comments. To insert text as a C++-style comment, simply precede the text with `//` and follow the text with the new line character.

All comments are removed from the program at [translation phase 3](https://devdocs.io/c/language/translation_phases) by replacing each comment with a single white space character.

### White Spaces

White spaces are non-printable characters that we use to write clear code. 

Space, horizontal and vertical tab, newline, form feed and carriage return are the white spaces available in C.

## Declaration

A declaration introduces one or more identifiers (variables) into the program and specifies their meaning and properties. It may appear in any scope.

Example: consider this declaration,

`int i = 3;`

This declaration tells the compiler to:

- Reserve space in memory to hold an integer value of type `int`. (specifier)
- Associate the name `i` with this memory location. (declarator)
- Store the value 3 at this location. (optional initializer)

Formally, each declaration consists of two distinct parts:

`specifiers-and-qualifiers` `declarators-and-initializers` `;`

where,

- `specifiers-and-qualifiers` are a list of type specifiers, type qualifiers and storage-class specifiers.
- `declarators-and-initializers` are a comma-separated list of declarators (the variables we are declaring). They may be accompanied by initializers.

An examples of declaration with parts labelled:

```c
extern long int a = 10, b = 20;
// |    |    |  ^-------^------ declarators with initialization
// |    |	 |_type specifier
// |    |_type qualifier
// |_storage class specifier
```

Note that a declaration is not visible to declarations that came before it; for example:

```c
int x = 5;
int y = x + 10;
```

will work, but:

```c
int x = y + 10;
int y = 5;
```

will not.

## Expressions

An expression is a sequence of operators (also functions) and their operands, that specifies a computation.

Expression evaluation may have the following effects:

- It may produce a result (e.g., evaluation of `2+2` produces the result `4`). 
- It may generate side-effects (e.g. evaluation of `printf("%d",4)` sends the character `'4'` to the standard output stream)
- It may designate objects or functions.

Each expression in C (an operator with its operands, a function call, a constant, a variable name, etc) is characterised by two independent properties: a **type** and a **value category**.

[See more about value category.](#value-categories-of-expressions)

## Compound Statement

A compound statement, or block,  groups multiple statements and declarations together to form a unit which is syntactically equal to a single statement. 

To make a compound statement we wrap statements and declarations in braces (i.e. `{` and `}`).

```c
// a compund statement
{
    declaration1;
    declaration2;
    statement1;
    statement2;
}
```

The braces that surround the statements of a function are one obvious example; braces around the statements after an `if`, `else`, `while` or `for` are another.

There is no semicolon after the right brace that ends a block.

## Type Conversion

Type conversion means change of the data type of an object or expression to another compatible type.

If the object or expression has greater range and precision than the type it's being converted to, then the range and precision are stripped off to match the target type.

Following are the two types of conversion that may happen:

### Implicit Conversion

When an expression is used in the context where a value of a different type is expected, conversion may occur. This conversion is automatic and happens only if the expected type is compatible with the evaluated value.

Following are some scenarios where implicit conversions takes place:

- Assignment

  ```c
  int n = 1L; // expression 1L has type long,
              // int is expected
  n = 2.1; // expression 2.1 has type double,
           // int is expected
  ```

- Passing arguments to functions

  ```c
  void f(double x) {
      printf("%lf \n", x) // -> 10.000000 
  }
  
  void main(void) {
      f(10); // 10 is converted to 10.000000
  }
  ```

- Arithmetic operations

  ```c
  1.f + 20000001; // -> 20000000.000000
  ```

  Here, `int` is converted to `float`, giving `20000000.00`. Adding 1 and then rounding to float gives `20000000.00`.

- Memory allocation

  ```c
  char *p = malloc(10); // expression malloc(10)
                        // has type void*,
  					 // char* is expected
  ```

###  Explicit Conversion /Casting

If type conversion of an object or expression is explicitly coded in the program (forced by the programmer), then its called explicit conversion or casting.

Explicit type conversion is done using the cast operator `()`.

`(type-name) expression`

where, `type-name` is either `void` or a scalar type and `expression` is of scalar type.

Some rules of casting are given below:

- If type-name is `void`, then expression is evaluated for its side-effects and its returned value is discarded.
- If type-name is exactly the type of expression, nothing is done.
- Otherwise, the value of expression is converted to the type named by type-name, as follows:
  - Any integer can be cast to any pointer type. Except for the null pointer constants such as `NULL`.
  - Any pointer type can be cast to any integer type.
  - Any pointer to object can be cast to any other pointer to object. If the value is not correctly aligned for the target type, the behavior is undefined.
  - Any pointer to function can be cast to a pointer to any other function type.
  - When casting between pointers (either object or function), if the original value is a null pointer value of its type, the result is the correct null pointer value for the target type.

 <div style="page-break-after: always; break-after: page;"></div>

# Appendix

## Value Categories of Expressions

Every expression belongs to one of three value categories: lvalue, non-lvalue object (rvalue), and function designator.

### Lvalue

Lvalue expression is any expression which potentially designates an object. It can be of any type except `void`. In other words, an lvalue expression evaluates to the object identity. 

The following expressions are lvalues:

- identifiers, including function parameters, provided they were declared as designating objects (not functions or enumeration constants)
- string literals
- compound literals
- parenthesised expression if the un-parenthesised expression is an lvalue
- the result of a member access (dot) operator if its left-hand argument is lvalue
- the result of a member access through pointer `->` operator
- the result of the de-reference (unary `*`) operator applied to a pointer to pointing to an object.
- the result of the subscription operator (`[]`)

### Non Lvalue

Non-lvalue expressions are the expressions of object types that do not designate objects, but rather values that have no object identity or storage location. The address of a non-lvalue object expression cannot be taken.

The following expressions are non-lvalue object expressions:

- integer, character, and floating constants
- all operators not specified to return lvalues, including
- - any function call expression
  - any cast expression (note that compound literals, which look similar, are lvalues)
  - member access operator (dot) applied to a non-lvalue structure/union, `f().x`, `(x,s1).a`, `(s1=s2).m`
  - all arithmetic, relational, logical, and bitwise operators
  - increment and decrement operators (note: pre forms are lvalues in C++)
  - assignment and compound assignment operators (note: they are lvalues in C++)
  - the conditional operator (note: may be lvalue in C++)
  - the comma operator (note: may be lvalue in C++)
  - the address-of operator, even it if is neutralised by being applied to the result of the unary `*` operator

As a special case, expressions of type `void` are assumed to be non-lvalue object expressions that yield a value which has no representation and requires no storage.

### Function Designator

A function designator (the identifier introduced by a function declaration) is an expression of function type. Note that the function-call operator is defined for pointers to functions and not for function designators themselves.

 