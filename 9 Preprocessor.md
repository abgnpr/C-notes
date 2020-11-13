# Preprocessing

There are several steps involved from the stage of writing a C program to the stage of executing it.

*Source code* -> **Preprocessor** -> *Extended Source Code* -> **Compiler** -> *Object Code* -> **Linker** -> *Executable Code*

**Preprocessing** is the first step a source file undergoes when we issue the compile command (`gcc myprog.c`). In this step, a program called the *preprocessor* modifies and expands the source code according to the preprocessing directions given within the code.

Preprocessing directions are given using the **preprocessing language**, which consists of *directives* to be executed and *macros* to be expanded. Lines beginning with `#` form the statements of the preprocessing language.

## Preprocessor

The preprocessor program is a part of the compiler tool chain which modifies a source code file according to the preprocessing directions in it before handing it over to the compiler. 

It takes a `.c` source file as input and gives the preprocessed `.i` file as output.

Its primary capabilities are:

- **Inclusion of header files** 

  These are files of declarations that can be substituted into your program.

- **Macro expansion**

  You can define *macros*, which are abbreviations for arbitrary fragments of C code. The preprocessor will replace the macros with their definitions throughout the program. Some macros are automatically defined for you.

- **Conditional compilation**

  You can include or exclude parts of the program according to various conditions.

- **Line control**

  If you use a program to combine or rearrange source files into an intermediate file which is then compiled, you can use line control to inform the compiler where each source line originally came from.

- **Diagnostics**

  You can detect problems at compile time and issue errors or warnings.

## Directives

Directives (preprocessing directives) control the behavior of the preprocessor. Each directive occupies one line and has the following format:

- `#` character
- preprocessing instruction (one of `define`, `undef`, `include`, `if`, `ifdef`, `ifndef`, `else`, `elif`, `endif`, `line`, `error`, `pragma`)
- arguments - which may contain preprocessor identifiers and fragments of c code (depends on the instruction)
- line break

Note: The null directive (`#` followed by a line break) is allowed and has no effect. and, preprocessor directives do not require semi-colon as a statement terminator.

#### Macro

A macro is a fragment of code which has been given a name. Whenever the name is used, it is replaced by the contents of the macro.

You may define any valid identifier as a macro, even if it is a C keyword. The preprocessor does not know anything about keywords. This can be useful if you wish to hide a keyword such as `const` from an older compiler that does not understand it. However, the preprocessor operator `defined` can never be defined as a macro.

There are two kinds of macros. They differ mostly in what they look like when they are used. [Object-like macros](#Object-like-macro) resemble data objects when used, [function-like macros](#Function-like macro) resemble function calls.

##### Object-like Macro

An *object-like macro* is a simple identifier which will be replaced by a code fragment. It is called object-like because it looks like a data object in code that uses it. They are most commonly used to give symbolic names to numeric constants.

We create macros with the `#define` directive. `#define` is followed by the name of the macro and then the token sequence it should be an abbreviation for, which is variously referred to as the macro's body, expansion or replacement list. For example,

`#define BUFFER_SIZE 1024`

```c
#define SIZE 5
#define ELEMENTS {1, 2, 3, 4, 5}
#define FRUIT "orange"

int arr[SIZE] = ELEMENTS;
char *fruit_name = FRUIT;
```



##### Function-like Macro

We can also define macros whose use looks like a function call. These are called *function-like macros*. To define a function-like macro, we use the same `#define` directive, but we put a pair of parentheses immediately after the macro name.

The syntax of a function-like macro invocation is similar to the syntax of a function call: each instance of the macro name followed by a `(` token as the next preprocessing token introduces the sequence of tokens that is replaced by the replacement-list. The sequence is terminated by the matching `)` token, skipping intervening matched pairs of left and right parentheses.

The number of arguments must be the same as the number of arguments in the macro definition (parameters) or the program is ill-formed.

```c
#include <stdio.h>

#define min(m, n) (m < n) ? m : n;
#define rep(p, q) for (int i = p; i <= q; ++i)

void main()
{
  rep(1, 10) { // replaced with -> for (int i = 1; i <= 10; ++i)
      printf("John Doe");
  }   
  
  int minimum = min(100, 90); // minimum = 90
  printf("%d\n", minimum); // -> 90
}
```



#### Macro Identifiers

These are identifiers used in macro definitions. Their properties are as follows:

- They are not variables and cannot be changed by your program code like variables. You generally use them when creating constants that represent numbers, strings or expressions.

- Most C programmers define their macro identifier names in uppercase, but it is not mandatory.

- An expression whose value is to be assigned to a macro identifier must be enclosed in parentheses if it contains operators.



### `#define`

Usage syntax

`#define identifier replacement-list`

`#define identifier( parameters, ... ) replacement-list`

The `#define` directive defines the `identifier` as a macro, that is it instructs the compiler to replace all successive occurrences of `identifier` with `replacement-list`, which can be optionally additionally processed.

If the identifier is already defined as any type of macro, the program is ill-formed unless the definitions are identical.

The first syntax behaves as Object-like macro. It replaces every occurrence of a defined `identifier` with `replacement-list`.

The second syntax behaves as a function-like macro where each occurrence of a defined `identifier` is replaced with `replacement-list`, additionally taking a number of arguments, which then replaces corresponding occurrences of any of the `parameters` in the `replacement-list`.



### `#undef`

If a macro ceases to be useful, it may be *undefined* with the `#undef` directive. `#undef` takes a single argument, the name of the macro to un-define. You use the bare macro name, even if the macro is function-like. It is an error if anything appears on the line after the macro name. `#undef` has no effect if the name is not a macro.

```c
#define FOO 4
  printf("%d\n", FOO); // -> 4

#undef FOO
  printf("%d\n", FOO); // -> error
```

Once a macro has been undefined, that identifier may be redefined as a macro by a subsequent `#define` directive. The new definition need not have any resemblance to the old definition.



### `#include`

Usage syntax:

`#include <filename>`

`#include "filename"`

First syntax searches for implementation-defined headers, meaning that it searches for the header files under control of the implementation. Typically only standard include directories (standard C library) are searched.

Second syntax searches for the header files that are not controlled by the implementation (user-defined or third-party libraries). Typically, the directory where the current file resides are searched for the mentioned headers and, only if the file is not found, the standard include directories are searched. Note that absolute or relative paths can also be used to locate the custom headers.

In the case the file is not found, the program is ill-formed.

```c
// implementation defined header (from std lib)
#include <stdio.h>

// user-defined or third-party header
#include "myUtilities.h" 

// a custom header located in the parent folder of the current folder
#include "../myCustomHeader.h"
```



### `#line`

Usage syntax:

`#line lineno`

`#line lineno "filename"`

First syntax changes the current preprocessor line number to `lineno`. Occurrences of the macro `__LINE__` beyond this point will expand to `lineno` plus the number of actual source code lines encountered since.

Second syntax changes the current preprocessor file name to `filename`, along with changing the line number to `lineno`. Occurrences of the macro `__FILE__` beyond this point will produce `filename`.

`lineno` must be a sequence of at least one decimal digit (the program is ill-formed, otherwise) and is always interpreted as decimal (even if it starts with `0`).

Any preprocessing tokens (macro constants or expressions) are permitted as arguments to `#line` as long as they expand to a valid decimal integer optionally following a valid character string.

```c
#line 50
#include <stdio.h>
void main() {
  printf("%d\n", __LINE__); // -> 54
}
```

This directive is used by some automatic code generation tools which produce C source files from a file written in another language. In that case, `#line` directives may be inserted in the generated C file referencing line numbers and the file name of the original (human-editable) source file.



### `#error`

Shows the given error message and renders the program ill-formed.

Usage syntax:

`#error error_message`

After encountering the `#error` directive, the preprocessor displays the diagnostic message `error_message` and renders the program ill-formed (the compilation stops).

`error_message` can consist of several words not necessarily in quotes.

Examples

```c
#if __STDC__ != 1
#  error "Not a standard compliant compiler"
#endif
 
#include <stdio.h>
int main (void)
{
    printf("The compiler used conforms to the ISO C Standard !!");
}
```

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

The preprocessor supports conditional compilation of parts of a source file. This behavior is controlled by `#if`, `#else`, `#elif`, `#ifdef`, `#ifndef` and `#endif` directives.

Usage syntax:

`#if expression`

`#ifdef identifier `

`#ifndef identifier `

`#elif expression`

`#else`

`#endif`

#### Structure

The conditional preprocessing block starts with `#if`, `#ifdef` or `#ifndef` directive, then optionally includes any number of `#elif` directives, then optionally includes at most one `#else` directive and is terminated with the `#endif` directive. Any inner conditional preprocessing blocks are processed separately.

Note that each `#if` directive in a source file must be matched by a closing `#endif` directive

Each of `#if`, `#elif`, `#else`, `#ifdef` and `#ifndef` directives control a code block until the first `#elif`, `#else`, `#endif` directive not belonging to any inner conditional preprocessing blocks.

#### How they work

`#if`, `#ifdef` and `#ifndef` directives test the specified condition, 

- `#if`, `#elif`

  Checks whether the value is true (everything but 0) and if so, includes the code until the closing `#endif`. If not, that code is removed from the copy of the file given to the compiler prior to compilation. There may be nested `#if` statements.

  ```c
  #if <value>
  /* code to execute if this value is true */
  #elsif lt;value>
  /* code to execute if this value is true */
  #else
  /* code to execut otherwise */
  #endif
  ```

- `#ifdef`

  Checks whether the given token has been `#defined` earlier in the file or in an included file. It is essentially equivalent to `#if defined`.

  ```c
  #ifdef <token>
  /* code */
  #else
  /* code to include if the token is not defined */
  #endif
  ```

- `#ifndef`

  Checks whether the given token has been `#defined` earlier in the file or in an included file. It is essentially equivalent to `#if !defined`.

  `#ifndef` is often used to make header files idempotent by defining a token once the file has been included and checking that the token was not set at the top of that file.

  ```c
  #ifndef <token>
  /* code */
  #else
  /* code to include if the token is defined */
  #endif
  ```



For the above three, if the given condition evaluates to true, then the following controlled block is compiled. In that case subsequent `#else` and `#elif` directives are ignored.

Otherwise, if the specified condition evaluates false, the controlled code block is skipped and the subsequent `#else` or `#elif` directive (if any) is processed. 

- In the former case, the code block controlled by the `#else` directive is unconditionally compiled. 
- In the latter case, the `#elif` directive acts as if it were a `#if` directive: checks for condition, compiles or skips the controlled code block based on the result, and in the latter case processes subsequent `#elif` and `#else` directives. 

The conditional preprocessing block is terminated by the `#endif` directive.

#####  *expression*

The expression is a constant expression, using only constants and identifiers, defined using ` #define` directive. Any identifier, which is not literal, non defined using ` #define` directive, evaluates to *0*.

The expression may contain unary operators in form `defined` identifier or `defined (`*identifier*`)` which return `1` if the identifier was defined using ` #define` directive and *0* otherwise. 

If the expression evaluates to nonzero value, the controlled code block is included, otherwise it is skipped. If any used identifier is not a constant, it is replaced with `0`.
