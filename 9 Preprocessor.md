# Preprocessing

There are several steps involved from the stage of writing a C program to the stage of executing it.

*Source code* -> **Preprocessor** -> *Extended Source Code* -> **Compiler** -> *Object Code* -> **Linker** -> *Executable Code*

**Preprocessing** is the first step a source file undergoes when we issue compile command (`gcc myprog.c`). In this step, a program called the *preprocessor* expands the source code according to the preprocessing directions given within the  code.

Preprocessing directions are given using the **preprocessing language**, which consists of *directives* to be executed and *macros* to be expanded. Lines beginning with `#` form the statements of the preprocessing language.

## Preprocessor

The preprocessor program is a part of the compiler tool chain. It takes a `.c` source file as input and gives the preprocessed `.i` file as output.

Its primary capabilities are:

- Inclusion of header files. These are files of declarations that can be substituted into your program.
- Macro expansion. You can define *macros*, which are abbreviations for arbitrary fragments of C code. The preprocessor will replace the macros with their definitions throughout the program. Some macros are automatically defined for you.
- Conditional compilation. You can include or exclude parts of the program according to various conditions.
- Line control. If you use a program to combine or rearrange source files into an intermediate file which is then compiled, you can use line control to inform the compiler where each source line originally came from.
- Diagnostics. You can detect problems at compile time and issue errors or warnings.

## Directives

The preprocessing directives control the behavior of the preprocessor. Each directive occupies one line and has the following format:

- `#` character
- preprocessing instruction (one of `define`, `undef`, `include`, `if`, `ifdef`, `ifndef`, `else`, `elif`, `endif`, `line`, `error`, `pragma`)
- arguments (depends on the instruction)
- line break

Note: The null directive (`#` followed by a line break) is allowed and has no effect.

Macro definitions are not variables and cannot be changed by your program code like variables. You generally use this syntax when creating constants that represent numbers, strings or expressions.

Most C programmers define their identifier names in uppercase, but it is not mandatory.

Expression whose value is assigned to the constant. The *expression* must be enclosed in parentheses if it contains operators.

Do NOT put a semicolon character at the end of #define statements. This is a common mistake.

### `#define`

Usage syntax

`#define identifier replacement-list`

`#define identifier( parameters, ... ) replacement-list`

The `#define` directives define the `identifier` as a macro, that is they instruct the compiler to replace all successive occurrences of `identifier` with `replacement-list`, which can be optionally additionally processed.

If the identifier is already defined as any type of macro, the program is ill-formed unless the definitions are identical.

#### Object-like macros

The first syntax behaves as Object-like macro. It replaces every occurrence of a defined `identifier` with `replacement-list`.

```c
#define SIZE 5
#define ELEMENTS {1, 2, 3, 4, 5}
#define FRUIT "orange"


int arr[SIZE] = ELEMENTS;
char *fruit_name = FRUIT;
```

#### Function-like macros

Function-like macros replace each occurrence of a defined `identifier` with `replacement-list`, additionally taking a number of arguments, which then replace corresponding occurrences of any of the `parameters` in the `replacement-list`.

The syntax of a function-like macro invocation is similar to the syntax of a function call: each instance of the macro name followed by a ( as the next preprocessing token introduces the sequence of tokens that is replaced by the replacement-list. The sequence is terminated by the matching ) token, skipping intervening matched pairs of left and right parentheses.

The number of arguments must be the same as the number of arguments in the macro definition (*parameters*) or the program is ill-formed.

```c
#include <stdio.h>

#define min(m, n) (m < n) ? m : n;
#define rep(p, q) for (int i = p; i <= q; ++i)

void main()
{
  rep(1, 10) { // for (int i = 1; i <= 10; ++i)
      printf("John Doe");
  }   
  
  int minimum = min(100, 90); // minimum = 90
  printf("%d\n", minimum); // -> 90
}
```



### `#include`

Usage syntax:

`#include <filename>`

`#include "filename"`

First syntax searches for the file in implementation-defined manner meaning that it searches for the files under control of the implementation. Typical implementations search only standard include directories (standard C library).

Second syntax searches for the file in implementation-defined manner. The intent of this syntax is to search for the files that are not controlled by the implementation. Typical implementations first search the directory where the current file resides and, only if the file is not found, search the standard include directories as with (1).

In the case the file is not found, the program is ill-formed.

### `#line`

Usage syntax:

`#line lineno`

`#line lineno "filename"`

First syntax changes the current preprocessor line number to `lineno`. Occurrences of the macro `__LINE__` beyond this point will expand to `lineno` plus the number of actual source code lines encountered since.

Second syntax changes the current preprocessor file name to `filename`. along with changing the line number to `lineno`. Occurrences of the macro `__FILE__` beyond this point will produce `filename`.

`lineno` must be a sequence of at least one decimal digit (the program is ill-formed, otherwise) and is always interpreted as decimal (even if it starts with `0`).

Any preprocessing tokens (macro constants or expressions) are permitted as arguments to `#line` as long as they expand to a valid decimal integer optionally following a valid character string.

```c

```

This directive is used by some automatic code generation tools which produce C source files from a file written in another language. In that case, `#line` directives may be inserted in the generated C file referencing line numbers and the file name of the original (human-editable) source file.

### `#error`

Shows the given error message and renders the program ill-formed.

Usage syntax:

`#error error_message`

After encountering the `#error` directive, an implementation displays the diagnostic message `error_message` and renders the program ill-formed (the compilation stops).

`error_message` can consist of several words not necessarily in quotes.

Example

```c
#ifndef __linux__
  #error "This isn't a linux OS"
#endif 

#ifndef _WIN32
  #error "This isn't a Windows OS"
#endif 

void main() {}
```



### Conditional compilation

#### `#if`

#### `#else`

#### `#elif`

#### `#ifdef`

#### `#undef`
