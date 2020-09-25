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

#### `for`

#### `while`

#### `do  –  while`

### Jumps

- `break`
- `continue`
- `goto`

