[toc]

# Basics

## Simple I/O

### Single character I/O

- `getch()`
- `getchar()`
- `getche()`
- `putchar()`

### Formatted I/O

- `printf()`
- `scanf()`

## Library Functions

Mathematical and Character functions

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

  - If it is a declaration, it is in scope in the entire loop body, including the remainder of `init_clause`, the entire `cond_expression`, the entire `iteration_expression` and the entire loop body.

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
      printf("%d ", n);
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

