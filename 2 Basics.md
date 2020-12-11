# Basics

---

## Console I/O

The screen and keyboard together are called a console. Using console I/O functions, we can receive input from the keyboard and send output to the screen

Console I/O can be divided in two categories — formatted and un-formatted.

### Formatted I/O

Formatted I/O functions let us fix the format of input and output.  `printf` and `scanf` are two most commonly used functions of this type.



#### `printf()`

`printf` function loads the data from the given locations (variables), converts them to character string equivalents and writes the results to `stdout`.

Prototype: `int printf( const char *format, ... );`

where, `format` is a pointer to a null-terminated character string specifying how to interpret the data.

The format string consists of conversion specifications and ordinary multi-byte characters (except `%`), which are copied unchanged into the output stream.

Each conversion specification has the following format:

- introductory `%` character
- (optional) one or more flags that modify the behavior of the conversion:
- - `-`: Make the result of the conversion is left-justified within the field (by default it is right-justified)
  - `+`: The sign of signed conversions is always prepended to the result of the conversion (by default the result is preceded by minus only when it is negative)
  - *space*: if the result of a signed conversion does not start with a sign character, or is empty, space is prepended to the result. It is ignored if `+` flag is present.
  - `0` : for integer and floating point number conversions, leading zeros are used to pad the field instead of *space* characters. For integer numbers it is ignored if the precision is explicitly specified. For other conversions using this flag results in undefined behavior. It is ignored if `-` flag is present.
- (optional) integer value or `*` that specifies minimum field width. The result is padded with *space* characters (by default), if required, on the left when right-justified, or on the right if left-justified. In the case when `*` is used, the width is specified by an additional argument of type `int`. If the value of the argument is negative, it results with the `-` flag specified and positive field width. (Note: This is the minimum width: The value is never truncated.)
- (optional) `.` followed by integer number or `*`, or neither that specifies *precision* of the conversion. In the case when `*` is used, the *precision* is specified by an additional argument of type `int`. If the value of this argument is negative, it is ignored. If neither a number nor `*` is used, the precision is taken as zero.
- conversion format specifiers. A list of format specifiers is given below.

Example

```c
#include <stdio.h>
 
int main(void)
{
    printf("Strings:\n");
    const char* s = "Hello";
    printf("\t.%10s.\n\t.%-10s.\n\t.%*s.\n", s, s, 10, s);
 
    printf("Characters:\t%c %%\n", 65);
 
    printf("Integers\n");
    printf("Decimal:\t%i %d %.6i %i %.0i %+i %i\n", 1, 2, 3, 0, 0, 4, -4);
    printf("Hexadecimal:\t%x %x %X %#x\n", 5, 10, 10, 6);
    printf("Octal:\t%o %#o %#o\n", 10, 10, 4);
 
    printf("Floating point\n");
    printf("Rounding:\t%f %.0f %.32f\n", 1.5, 1.5, 1.3);
    printf("Padding:\t%05.2f %.2f %5.2f\n", 1.5, 1.5, 1.5);
    printf("Scientific:\t%E %e\n", 1.5, 1.5);
    printf("Hexadecimal:\t%a %A\n", 1.5, 1.5);
}
```

Output

```
Strings:
    .     Hello.
    .Hello     .
    .     Hello.
Characters:     A %
Integers
Decimal:        1 2 000003 0  +4 -4
Hexadecimal:    5 a A 0x6
Octal:          12 012 04
Floating point
Rounding:       1.500000 2 1.30000000000000004440892098500626
Padding:        01.50 1.50  1.50
Scientific:     1.500000E+00 1.500000e+00
Hexadecimal:    0x1.8p+0 0X1.8P+0
```



#### `scanf()`

`scanf` function reads data from `stdin`, interprets it according to `format` and stores the results into given locations.

Prototype: `int scanf( const char *format, ... );`

where, `format` is a pointer to a null-terminated character string specifying how to read the input.

The format string consists of:

-  non white space multi-byte characters except `%`: each such character in the format string consumes exactly one identical character from the input stream, or causes the function to fail if the next character on the stream does not compare equal.
-  white space characters: any single white space character in the format string consumes all available consecutive white space characters from the input. There is no difference between `"\n"`, `" "`, `"\t\t"`, or other white space in the format string.
-  conversion specifications. Each conversion specification has the following format:
   -  introductory `%` character
   -  (optional) assignment-suppressing character `*`. If this option is present, the function does not assign the result of the conversion to any receiving argument.
   -  (optional) integer number (greater than zero) that specifies *maximum field width*, that is, the maximum number of characters that the function is allowed to consume when doing the conversion specified by the current conversion specification. Note that %s and %[ may lead to buffer overflow if the width is not provided.
   -  conversion format specifiers. A list of format specifiers is given below.

Example

```c
#include <stdio.h>

int main(void)
{
  int i, j, n_fields;
  float x, y;
  char str1[10];

  n_fields = scanf(
    "%d %f %9s %2d %f",
    &i, &x, str1, &j, &y
  );

  printf(
    "Converted %d fields:\n"
    "i = %d\n"
    "x = %f\n"
    "str1 = %s\n"
    "j = %d\n"
    "y = %f\n",
    n_fields, i, x, str1, j, y
  );
}
```

Input

```
25 54.32E-1 Thompson 56789
```

Output

```
Converted 5 fields:
i = 25
x = 5.432000
str1 = Thompson
j = 56
y = 789.000000
```



#### Conversion Format Specifiers

| Conversion specifier | Explanation                                                  |
| :------------------- | :----------------------------------------------------------- |
| `%c`                 | writes a **single character**.                               |
| `%s`                 | writes a **character string**.                               |
| `%d` `%i`            | converts a **signed integer** into decimal representation `[-]dddd`. |
| `%u`                 | converts an **unsigned integer** into decimal representation `dddd`. |
| `%o`                 | converts a **unsigned integer** into octal representation `oooo`. |
| `%x` `%X`            | converts an **unsigned integer** into hexadecimal representation `hhhh`. |
| `%f` `%F`            | converts **floating-point number** to the decimal notation in the style `[-]ddd.ddd`. |
| `%e` `%E`            | converts **floating-point number** to the decimal exponent notation. |
| `%g` `%G`            | converts **floating-point number** to decimal or decimal exponent notation depending on the value and the *precision*. |
| `%a` `%A`            | converts **floating-point number** to the hexadecimal exponent notation. |
| `%n`                 | returns the **number of characters written** so far by this call to the function. |
| `%p`                 | writes an implementation defined character sequence defining a **pointer**. |

##### Length modifiers

Length modifiers are prefixed to conversion specifiers to denote the variant of the basic type being used.

Examples

`%lld` for `long long int`

`%Lf` for `long double`

| modifier | `%c`                   | `%s`      | `%d`            | `%u`, `%o`, `%x`     | `%f`, `%e`, `%g`, `%a` |
| -------- | ---------------------- | --------- | --------------- | -------------------- | ---------------------- |
| `hh`     |                        |           | `signed char`   | `unsigned char`      |                        |
| `h`      |                        |           | `short`         | `unsigned short`     |                        |
| none     | `unsigned char`, `int` | `char*`   | `int`           | `unsigned int`       | `double`               |
| `l`      | `wint_t`               | `wchar_t` | `long`          | `unsigned long`      | `double`               |
| `ll`     |                        |           | `long long`     | `unsigned long long` |                        |
| `z`      |                        |           | signed `size_t` | `size_t`             |                        |
| `L`      |                        |           |                 |                      | `long double`          |

<div style="page-break-after: always; break-after: page;"></div>

### Single character I/O

#### `getchar()`

Reads the next character from `stdin`.

Prototype: `int getchar(void)`

Header: `stdio.h`

Returns the obtained character on success or `EOF` on failure.

Example

```c
#include <stdio.h>

// reads and prints a character
void main(void) {
  printf("Enter a character: ");
  char ch = getchar();
  printf("You entered: %c\n", ch);
}

/* Output: 
Enter a character: z
You entered: z
*/
```

#### `putchar()`

Writes a character `ch` to `stdout`. 

Internally, the character is converted to unsigned char just before being written.

Prototype: `int putchar( int ch );`, where `ch` is the character to be written.

Header: `stdio.h`

On success, returns the written character. On failure, returns `EOF` and sets the error indicator on `stdout`.

Example

```c
#include <stdio.h>

// prints letters from a to z (ascii 97 to 122)
int main(void) {
  for (char ch = 97; ch <= 122; ch++)
    putchar(ch);
  
  putchar('\n');
}

// output:
// abcdefghijklmnopqrstuvwxyz
```

#### `getch()`

The `getch`  function reads a single character from the console without echoing the character.

Prototype: `int getch(void);`

Header: `conio.h`

Returns the character read. There's no error return.

Example

```c
// This program reads characters from
// the keyboard until it receives a 'Y' or 'y'.
#include <conio.h>
#include <ctype.h>

int main( void )
{
   int ch;

   cputs( "Type 'Y' when finished typing keys: " );
   do
   {
      ch = getch();
      ch = toupper( ch );
   } while( ch != 'Y' );

   putch( ch );
   putch( '\n' );    // Line feed
}
```

#### `getche()`

The `getche` function reads a single character from the console with echo, meaning that the character is displayed at the console.

Prototype: `int getche(void);`

Header: `conio.h`

Returns the character read. There's no error return.

Example: Same as the example for `getch()`. Replace `getch()` with `getche()`. 

<div style="page-break-after: always; break-after: page;"></div>

## Control Flow

Control flow specifies the order in which computations are performed.

### Conditionals

Conditionals are used to express decision. They enable us to carry out tasks depending upon whether a task was fulfilled.

#### `if`

`if` statement evaluates the expression within its brackets; if it is true (that is, if the expression is a non-zero value), then the statement or the block of statements following it are executed.

```c
if (expression)
    statement;

// OR

if (expression) {
    statement1;
    statement2;
    // ...
}
```

#### `else`

`else` is an optional statement that goes after the body of `if`. When  `if` has an `else`  part following it and the expression in`if` is false, the statements given under `else` are executed.

```c
if (expression)
    statement;
else
    statement;

// OR

if (expression) {
    statement1;
    statement2;
} else {
    statement4;
    statement3;
}
```

Because the `else` part of an `if-else`	is optional, an ambiguity arises when an else is omitted from a nested `if` sequence. This is resolved by associating the `else` with the closest previous `else`-less `if`.

For example, in

```c
if (n > 0)
    if (a > b)
        z = a;
	else
        z = b;
```

the `else` goes to the inner `if`, as shown by indentation. If that isn't desired, let's say you want to associate `else` with outer `if`, then you must use brace to force proper association like so

```c
if (n > 0) {
    if (a > b)

} else
    z = b;
```

 #### `else if`

`if` and `else` statements can be sequenced to form a *conditional ladder*.

```c
if (expression)
    statement;
else if (expression)
    statement;
else if (expression)
    statement;
else if (expression)
    statement;
else
    statement;
```

This is the most general way of writing a multi-way decision.

The expressions are evaluated in order; if an expression is true, the statements associated with it is executed, and this terminates the whole chain.

The last `else` handles the "none of the above" or default case where none of the other conditions is satisfied. Sometimes there is no explicit action for the default; in that case the trailing `else` and its statement can be omitted, or it may used for error checking to catch an "impossible" condition.

The code for each statement is either a single statement, or a group of them in braces.

Here's an example of using `if - else if - else` ladder

```c
/* binary search
 * find x in v[0] <= v[1] <= ... <= v[n-1] */
it binsearch (int , int v[], int n) {
    int low, high, mid;
    
    low = 0;
    high = n - 1;
    while (low <= high) {
        mid = (low + high) / 2;
        if (x < v[mid])
            high = mid - 1;
        else if (x > v[mid])
            low = mid + 1;
        else // found match
            return mid;
    }
    
    return -1; // no match
}
```

The fundamental decision is whether x is less than, greater than, or equal to the middle element `v[mid]` at each step; this is a natural case for  `if - else if - else` .

#### `? :` (Conditional Operator)

Conditional operator `? :` acts like an `if-else` block. 

First, it evaluates `condition`. If the result of `condition` compares unequal to zero, executes `expression-true`, otherwise executes `expression-false`.

```c
condition ? expression-true : expression-false;
```

where, `condition` is a scalar expression, `expression-true` is the expression that will be evaluated if condition is not equal to zero and `expression-false` is the expression that will be evaluated if condition is equal to zero.

Result from either expression can be stored into a variable.

``` c
// absolute value of var is stored in result
int result = var < 0 ? -var : var;
```

Since the operator operates on  3 operands, it's a *ternary operator*.

Conditional operator has right-to-left associativity, which allows chaining.

```c
struct vehicle v = arg == 'B' ? bus      :
                   arg == 'A' ? airplane :
                   arg == 'T' ? train    :
                   arg == 'C' ? car      :
                   arg == 'H' ? horse    :
                                feet;
```

#### `switch...case`

The switch statement is a multi-way decision that tests whether an expression matches one of a number of constant integer values, and branches accordingly.

```c
switch (expression) {
    case const_expr: 
        statements;
        break;
    case const_expr:
        statements;
        break;
    default: 
        statements;
        break; // defensive; not necessary
}
```

- Each case is labelled by one or more integer-valued constants or constant expressions. 
- All case expressions must be different.
- If a case matches the expression value, execution starts at that case. 
- The `break` statement causes an immediate exit from the `switch`. Because cases serve just as labels, after the code for one is done, execution *falls through* to the next unless you take explicit action to escape (using `break` or `return`)
- The case labelled `default` is executed if none of the other cases are satisfied. It is optional; if it's absent and if none of the cases match , no action takes place.

<div style="page-break-after: always; break-after: page;"></div>

### Loops

Loop statements are used to repeat a statement or a block depending upon some condition.

#### `for`

Executes a `statement` or a block of statements (loop body) repeatedly until the value of `cond_expression` becomes false. The test takes place before each iteration.

```c
for (init_clause; cond_expression; iteration_expression)
    statement;

// OR

for (init_clause; cond_expression; iteration_expression) {
    statement1;
    statement2;
}
```

**Working:**

- As soon as the `for` statement is seen, the`init_clause` is executed. It may be an expression or a declaration

  - If it is an expression, it is evaluated once and its result is discarded.

  - If it is a declaration, it is in scope in the entire loop body, including the remainder of `init_clause`, the entire `cond_expression`, and the entire `iteration_expression`.

- `cond_expression` is evaluated next.
- If it evaluates to true, execution of the loop body follows.
  - If the result of the expression is zero, the loop statement is exited immediately.
  
- `iteration_expression` is evaluated after the loop body and its result is discarded. 

- After evaluating `iteration_expression`, control is transferred to `cond_expression`.

**Example:**

```c
/* prints numbers 1 to 10 */
for (int i = 1; i <= 10; ++i) {
    printf("%d ");
}
```

**Note:**

- `init_clause`, `cond_expression`, and `iteration_expression` are all optional:

  ```c
  for(;;) {
      printf("endless loop!");
  }
  ```

- `statement` is not optional, but it may be a null statement:

  ```c
  for(int n = 0; n < 10; ++n, printf("%d\n", n))
      ; // null statement
  ```

- If the execution of the loop needs to be terminated at some point, a `break` statement can be used anywhere within the loop body. The continue statement used anywhere within the loop body transfers control to `iteration_expression`.

- `for` is used when we want to keep the loop control statements close together and visible at the top of the loop. The advantage of keeping loop control centralised are obvious when there are several nested loops.

- It is possible to place multiple expressions in various parts of `for` statement using the comma `,` operator[^*], for example to process two indices in parallel.

  ```c
  #include<string.h>
  
  /* reverse: reverse string s in place */
  void reverse(char s[]) {
      char temp;
      int i, j;
      for (i = 0, j = strlen(s) - 1; i < j; i++, j--) {
          temp = s[i];
  		s[i] = s[j];
          s[j] = c;
      }
  }
  ```

  [^*]:A pair of expressions separated by a comma is evaluated left to right, and the type and value of the result are the type and value of the right operand.


#### `while`

Executes a `statement` or a block of statements (also called the loop body) repeatedly until the value of `expression` (also called controlling expression) becomes false. The test takes place before each iteration.

```c
while (expression)
    statement;

// OR

while (expression) {
    statement1;
    statement2;
}
```

- The repetition occurs regardless of whether the loop body is entered normally or by a `goto` into the middle of statement.

- The evaluation of expression takes place *before* each execution of statement (unless entered by a `goto`).

- If the execution of the loop needs to be terminated at some point, `break` statement can be used as a terminating statement. If the execution of the loop needs to be `continued` at the end of the loop body, continue statement can be used as a shortcut.

- An endless loop can be created like this

  ```c
  while (1) {
      statement;
  }
  ```


#### `do  –  while`

Executes a `statement` or a block of statements (loop body) repeatedly until the value of `expression` becomes false. The test takes place after each iteration.

```c
do statement while (expression);

// OR

do {
    statement1;
    statement2;
} while (expression);
```

- The repetition occurs regardless of whether the loop body is entered normally or by a `goto` into the middle of statement.

- The evaluation of expression takes place *after* each execution of statement.  (whether entered normally or by a `goto`).

- If the execution of the loop needs to be terminated at some point, `break` statement can be used as terminating statement. If the execution of the loop needs to be continued at the end of the loop body, `continue` statement can be used as a shortcut.

- An endless loop can be created like this

  ```c
  do {
  	statement;
  } while (1);
  ```


<div style="page-break-after: always; break-after: page;"></div>

### Jumps

#### `break`

Used to terminate the enclosing for, while or do-while loop or switch statement.

`break;`

- It appears only within the statement of a loop body (while, do, for) or within the statement of a switch.

- After this statement the control is transferred to the statement or declaration immediately following the enclosing loop or switch.

- A break statement cannot be used to break out of multiple nested loops. The `goto` statement may be used for this purpose.

- Usage tip: Use when it is otherwise awkward to ignore the remaining portion of the loop using conditional statements.

- Example

  ```c
  // prints integers 10 to 5
  int n = 10;
while (1) {
      printf("%d ", n--);
      if (n == 5)
          break;
  }
  ```
  
  

#### `continue`

Causes the remaining portion of the enclosing for, while or do-while loop body to be skipped.

`continue;`

- It appears only within the loop body of for, while, and do-while loops.

- The `continue` statement causes a jump, as if by `goto`, to the end of the loop body.

- Usage tip: Use when it is otherwise awkward to ignore the remaining portion of the loop using conditional statements.

- Example

  ```c
  // Prints all numbers from 1 to 10, except 6
  for (int i = 1; i <= 10; ++i) {
    if (i == 6)
          continue;
      printf("%d ", i) // skipped when i = 6
  }
  ```
  
  

#### `goto`

`goto` with `labels` is used to to transfer control unconditionally to the desired location.

`goto label;`

`label: statement`

The `goto` statement causes an unconditional jump (transfer of control) to the statement prefixed by the named `label` (which must appear in the same function as the `goto` statement).

`label`:

- A `label` is an identifier followed by a colon `:` and a statement. 

- Labels are the only identifiers that have function scope: they can be used (in a `goto` statement) anywhere in the same function in which they appear. 

- There may be multiple labels before any statement.

- A label before a declaration must use a null statement (a semicolon immediately after the colon) because declarations are not statements. Same applies to a label before the end of a block.

Example

```c
#include <stdio.h>
 
int main(void)
{
    // goto can be used to leave a multi-level loop easily
    for (int x = 0; x < 3; x++) {
        for (int y = 0; y < 3; y++) {
            printf("(%d;%d)\n",x,y);
            if (x + y >= 3)
                goto endloop;
        }
    }
	
    endloop:;
}
```



## Library Functions

Library functions are the built-in ready made functions. We can use them in our code to do common tasks without worrying about details.

An excellent example is the `printf` function. It prints to the standard output of the operating system without our having to worry about how the printing work is done.

Prototypes and definitions of library functions are present in header files. To use a function, we just need to add the appropriate header in our program.

Examples

- Arithmetic functions

  `abs`, `log`, `exp`, `sin`, `pow` etc..

- Date conversion functions

  `atoi` (converts `string` to `int`)

  `strtol` (converts `string` to `long`)

  `fcvt` (converts `double` to `string`)

  etc..

- Character classification functions

  `isalnum` (tests for alphanumeric character)

  `isdigit` (tests for decimal digit)

  `isspace` (tests) for white space character

  etc..

- String manipulation functions

  `strcat` (appends one string to another)

  `strcmp` (compares two strings)

  `strlen` (finds length of a string)

  etc..

- Searching and Sorting

  `bsearch` (performs binary search)

  `qsort` (performs quick sort)
  
- Console I/O function

  `printf` (formatted output)

  `scanf` (formatted input)

  `putchar` (un-formatted single character output)

  `getchar` (un-formatted single character input) 