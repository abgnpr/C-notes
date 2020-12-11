# Functions

A function is a construct that associates a compound statement (the function body) with an identifier (the function name). When we want to execute the function, we call it using its name and then the steps given in its body are performed.

Using a function is like hiring a person to do a specific job for you. Sometimes the interaction with this person is simple; sometimes it's complex.

## Need

- **Reuse**

  Functions enable code re-use. It saves us from the pain of writing the same code again and again. If we need to write a chunk of code multiple times in our program, for example a piece of code for finding the length of a string, we can wrap it inside a function and then call the function multiple times from anywhere in our program.

  Re-usability also enables us to use a single function in several different (and separate) programs. When you need to write a new program, you can go back to your old programs, find the functions you need, and reuse those functions in your new program. You can also reuse functions that somebody else has written for you (libraries).

- **Abstraction**

  If you want to use a ready made function in your program, you don't have to know how it works inside! You don't have to understand anything about what goes on inside the function. All you need to know is the function name, what it does, what input it takes and the kind of result it gives.

  It's sort of like driving a car; you don't need to understand every detail about the engine and drive train and wheels, if all you want to do is drive the car.

  This approach of hiding away the details from the user is called abstraction and it goes a long way in boosting the user's productivity and saves his time. 

- **Modularity**

  Using functions, we can do modular programming. In this approach we separate the functionality of a program into independent units (functions), such that each unit has everything necessary to fulfil one purpose. These units are the building blocks of the program and they work together to achieve a common goal.

- **Clarity**

  Splitting the program into small independent chunks makes it easier to read, understand and modify. The flow and logic becomes much more clear. Anyone who reads the program code later on will easily understand the thought process of the programmer who created it. 

## Defining a Function

A function definition comprises the function's name, the type of values it'll accept, the tasks it'll do and it's return type.

Each function must be defined only once in a program.

```c
/* Sample Function definition.
Defines a function with the name "sum"
and with the body "{ return x + y; }" */
int sum(int x, int y)
{
    return x + y;
}
```

```c
/* Parts of a function definition labelled
vvv---return type  */
int sum(int x, int y) // <-- parameters
//  ^^^---function name
{   // body
    return x + y; // result
}
```

The various parts in a function definition are as follows.

- **Name:** is the identifier with which we'll call and use the function when required.

- **Parameters:** are identifiers that specify the type and number of values that a function will accept. We can also say that parameters are variables in which the function receives and stores the data that's supplied to it and later on operates on them to perform some tasks. 

  - Parameters, along with their respective types, are written in brackets `()` after the function name.
  - A function accepts values in the order of the specified parameters. If the values supplied do not match in type, order or number, it gives an error.
  
  - Parameters have meaning only inside the function to which they belong, which means they are local to the function. 
  - Any change to the parameters inside the function do not have any effect on the values or variables of the caller function.   
  
- **Body:** is a compound statement that holds the steps to achieve the goal of the function. It may have a return statement, which is necessary if the function is expected to give some result back to the caller. 

- `return`: is a keyword used inside the body to send a value (result, status, error etc.) back to the caller. It also terminates the current function.

  - There can be more than one `return` in a function.
  - `return` need not always be present at the end of the function body.

  [See more on `return`](#more-on-return)

- **Return type:** indicates the data type of the return value. 

  The default return type of C functions is `int`.  This is why we are allowed to omit the return type when we want it to be an `int`. However, this behaviour is now deprecated and generates a compiler warning. It is recommended that we explicitly mention the return type of each function. 

  ```c
  // works, but gives a warning 
  main() { }
  ```

  ```c
  // recommended way
  void main() { }
  ```

## Using a Function (Function Call)

To use a function we have to call it by writing the function name with the *function call operator* `()` followed by a semicolon. Within the function call operator, we can supply zero or more arguments.

Arguments: are variables, constants or expressions that are used to initialise the function's parameters. Order and type of the arguments must match with those of the function parameters.

The function call expression has the form:

`function-name(argument-list);`

As an example, let's call the function `sum` we defined above.

```c
// parameters x and y are initialized with the arguments 1 and 2
int s = sum(1, 2); // value of s becomes 3
```

We have called the function `sum` by writing its name with brackets `()`, and within the brackets we have supplied the arguments  `1` and `2` .  We have also assigned the function call to a new variable `int s` so that the value returned gets stored in it.

### Calling Convention

Calling convention indicates the order in which arguments are passed to a function when a function call is encountered. C language follows <u>right to left</u> calling convention.

In most cases, it doesn't matter which way the arguments are passed, however in some functions it may be an important consideration.

For example, the call to `printf` here is expected to output `1 2 3`.

```c
int a = 1;
printf("%d %d %d\n", a, ++a, a++); // expected -> 1 2 3 | actual -> 3 3 1
```

But surprisingly, it outputs `3 3 1`. This is because C's calling convention is from right to left.

Explanation:

`1` is passed through the expression `a++` and then `a` is incremented to `2`. Then result of `++a` is passed. That is, `a` is incremented to 3 and then passed. Finally, latest value of `a` i.e. `3`, is passed. Thus in right to left order `1, 3, 3` gets passed. After collecting the values, `printf` prints them in left to right order since we have asked it to do so. This gives us `3 3 1`.

## More on `return`

- Whenever the control returns from a function, some value is definitely returned. If it's a meaningful value, we accept it in the calling function by equating the called function to a variable. The variable's type must match with the return type of the called function.

  ```c
  int s = sum(a, b);
  ```

- If we do not want a called function to return any value, we can put the keyword `void` as the return type of that function.

  ```c
  void sayHolla() {
      printf("Holla!\n"); // simply does the work and exits; returns nothing
  }
  ```

- A function can return only one value at a time.

  ```c
  return a+b; // good
  return (a+b, a-b) // bad!; trying to return multiple values
  ```

  We can get around this limitation by wrapping multiple values inside a `struct `and then return it.

## Types of Functions

### `main()`

Every C program contains the definition of a function called `main`. It is the designated start of the program, which means that the program begins execution from the main function. It either terminates, or invokes other, user-defined or library functions.

Corollary: Any C program contains at least one function and if a program contains only one function, it must be `main()`.

There are different ways of defining main. Here are the few most commonly used.

```c
void main(void) {
    // body
}
```

```c
int main(void) {
    // body
    return 0;
}
```

We can leave out the `void` keyword because empty `()` will work in the same way.[^1]

```c
int main() {
    // body
    return 0;
}
```

To make a program accept command line arguments, we have some special parameters: `int argc` and `char *argv[]`.

```c
int main(int argc, char *argv[]) {
    // body
    return 0;
}
```

where, `argc` (arguments count) is the number of arguments passed to the program and `argv` (argument vector) is a pointer to the first element of an array of `argc + 1` pointers. The first element of this array `argv[0]` points to a string representing the name of the program and the rest, if any, point to strings that represent the arguments passed to the program.

```c
#include <stdio.h>
void main(int argc, const char *argv[])
{
  for (int i = 0; i < argc; i++) {
    fputs(argv[i], stdout);
    putchar('\n');
  }
}
```

[^1]: the declarators `f()` and `f(void)` have different meaning: the declarator `f(void)` is a new-style (prototype) declarator that declares a function that takes no parameters. The declarator `f()` is an old-style (K&R) declarator that declares a function that takes *unspecified* number of parameters.

### User-defined Functions

User-defined functions (UDFs) are functions that programmers create for their own needs. 

- The name of a user-defined function can be any anything except keywords and `main` .
- There is no limit on the number of user defined functions that might be present in a C program.

There are two places we can put UDFs inside a program; although where you want put it is entirely up to you.

- **In the global declaration section (before  `main`)**

  We can simply define functions in the global declaration section and then use them inside the `main` function present below. The following example shows how to define function in the global declaration section.

  ```c
  // LINK SECTION
  // include headers...
  
  // GLOBAL DECLARATION SECTION <- function defintion goes here
  int dummy(int x, int y) {
      // do dummy things
      return 0;
  }
  // other UDF definitions...
  
  // MAIN SECTION
  int main() {
      dummy(); // calls dummy
  }
  ```

- **After `main`**

  If we decide to define our functions after `main`, we must first put the respective *function prototypes* in the global declaration section and then put their definitions after the body of `main`.

  A function prototype is a signature that is used to identify the function. It comprises the <u>return type</u> and the <u>function name</u> with <u>parameter types</u> within brackets(no identifiers needed), followed by a <u>semicolon</u>.

  ```c
  // Function declaration
  int dummy(int, int); 
  ```

  The following code shows how to define functions with prototypes:

  ```c
  // LINK SECTION
  // include headers...
  
  // GLOBAL DECLARATION SECTION <- function prototypes go here
  int dummy(int, int);
  // other UDF prototypes...
  
  // MAIN SECTION
  int main() {
      dummy(); // calls dummy
  }
  
  // UDF SECTION <- function definitions go here
  int dummy(int x, int y) {
      // do dummy things
      return 0;
  }
  
  // other UDF definitions...
  ```

### Library Functions

Library functions are commonly required functions grouped together and stored in a bunch of header files on the disk. These are ready made pieces of code written for us by people who make the language compiler. A standard set of such functions, called the standard library, is available in all programming environments where the C compiler tool chain is present.

## Nesting

Nesting of functions means defining and using functions within functions.

A nested function can be used only within the function it is defined.

Here's an example: a function named `inner` is defined and called inside another function named `outer`, and `outer` is defined and called inside `main`.

Function calls take place in this order:

OS  –calls-->  `main()`  –calls-->  `outer()`  --calls-->  `inner()`  

```c
#include <stdio.h>
int main(void)  { // -> called by operating system
	printf("Inside main()\n");
  
	int outer() {
    	printf("Inside outer()\n");
    	
        int inner() {
      		printf("Inside inner()\n");
      		printf("Exited inner()\n");
    	}
    
    	inner(); // -> called by outer()
    
    	printf("Exited outer()\n");
  	}

  	outer(); // -> called by main()
  
    // inner(); // -> error; main can't find where inner is. 
    
  	printf("Exited main()\n");
}
```

Output

```
Inside main()
Inside outer()
Inside inner()
Exited inner()
Exited outer()
Exited main()
```

## Passing Objects to Functions

For most functions to work we need to give them some input, which we provide as arguments during a function call. Arguments are nothing but some values that we pass to a function to operate upon. The arguments we supply are copied into the respective parameters of the called function and then the function uses those parameters to perform some task.

There are two ways to pass values to a function:

- pass by value, and
- pass by reference

### Pass by Value

In *pass by value* we pass an object of any basic or user defined type (like `int`, `float`, `struct`, etc) to the called function. In passing this way, a copy of the object (a duplicate stored at a different memory location) is given and not the original object. Any changes made to it inside the called function will not be reflected in the caller.

Here's an example: On calling `add`, the variables `a` and `b` are copied to `x` and `y` respectively. Although `x` is altered inside `add`, it has no effect on the value of `a` in the caller function(i.e. `main`).

```c
#include <stdio.h>

int add(int x, int y) { // x & y receive copied values from a & b
    x += y;
    return x;
}

void main() {
    int a = 10;
    int b = 20;
    int sum = add(a, b); // values of a & b are copied to x & y and then added
	printf("Sum of %d and %d = %d\n", a, b, sum); //-> Sum of 10 and 20 = 30
}
```

```
Sum of 10 and 20 = 30
```

### Pass by Reference

In *pass by reference* we <u>pass the address (pointer) of an object</u>, which means that we pass a value that is not the object itself but a reference to it. Sure the address / reference we are passing is another object on its own and it gets passed by value and thus copied, but no copies of the original object are created. There exists only one instance of the original object in memory and by using the reference(address), the called function can directly manipulate it and changes will be visible everywhere.

```c
#include <stdio.h>

// changes negative integers to positive
void make_positive(int *n) { // *n refers to a
  	if (*n < 0)
    	*n = -*n;
}

void main(void) {
	int a = -10;  
  	make_positive(&a); // address of a is passed
    
  	// changes made to a in make_positive() are visible here
    printf("%d\n", a); // -> 10
}
```

#### Passing Arrays

Pass by reference is really helpful when we have to pass around big objects like arrays. Arrays can be quite large and passing them 'by value' would hamper performance since each pass would require the array to be copied. Hence C does not allow passing arrays 'by value'.

That leaves us with pass by reference. Since the name of an array is a pointer to its first element, we can pass it to other functions to serve as a reference for the array.

However, the passed reference won't give the array size on using `sizeof`  inside the called function, so we must supply the array size to the function as well.

Example

```c
#include <stdio.h>

// returns the sum of all elements of an array
int total(int arr[], int size) {
  int sum = 0;
  for (int i = 0; i < size; ++i)
    sum += arr[i];
  return sum;
}

void main(void) {
  int a[] = {1, 2, 3, 4, 5}; // variable a stores the address of a[0]
  int size = 5;

  int t = total(a, size);
  printf("Total = %d\n", t);
}
```

A parameter to receive arrays can be specified in two ways: (1) using `[]`, or (2) using `*`. The first way has been shown in the example above. We could've written the array parameter of `total`, using the second way, like this:

```c
int total(int *arr, int size) {
    // ...
}
```

Both ways are valid and mean the same thing.

## Recursion

Recursion, in general, is defining something in terms of itself. 

In programming, *recursion* occurs when a function calls itself. Thus, a function is called *recursive* if it calls itself. In other words, if a statement within the body of a function calls the same function then it's a recursive function.

The function `fn` given below is a recursive function. It has been programmed to make 5 subsequent calls to itself. First of all `main()` calls `fn()`, then the first  `fn` instance calls a second instance of `fn`, the second instance calls a third instance and so on till the fifth instance gets called. Since the fifth instance cannot call any more instances, it exits and returns back to the fourth instance. The fourth instance, having nothing else to do, also exits. Similarly, all instances exit and return back to the instance that called them and finally the control reaches `main` once again.

We have shown the subsequent calls and exits of `fn` instances in the output using `printf`.

```c
#include <stdio.h>

int counter = 0;
int indent = 0;

void fn(void) // recursive function
{
  int callNo = ++counter;

  indent += 5;
  printf("%*c\\__ fn call %d\n", indent, ' ', callNo);

  if (callNo < 5)
  {
    fn(); // recursive call
  }
  
  printf("%*c/-- fn exit %d\n", indent, ' ', callNo);
  indent -= 5;
}

void main(void)
{
  printf("  main\n");

  fn();

  printf("  main\n");
}
```

Output

```
  main
     \__ fn call 1
          \__ fn call 2
               \__ fn call 3
                    \__ fn call 4
                         \__ fn call 5
                         /-- fn exit 5
                    /-- fn exit 4
               /-- fn exit 3
          /-- fn exit 2
     /-- fn exit 1
  main
```

#### Finding Factorial using recursion

Next we have a program where we apply recursion to find the factorial of a number.

Recursive definition of a factorial is `factorial(n) = n x factorial(n-1)` with the base case `factorial(1) = 1`.

Implementation

```c
#include <stdio.h>
typedef unsigned long long ll; // factorials get pretty large, so we need a bigger type

ll factorial(ll n) { return (n == 1) ? 1 : (n * factorial(n - 1)); }
void main(void) { printf("Factorial of 20 = %llu\n", factorial(20)); }
```

 Output

```
Factorial of 20 = 2432902008176640000
```

`factorial()` makes multiple subsequent calls to itself until it hits the base case, from where it rolls up the call trace (exits instances in reverse order) and returns the factorial at each stage to the caller on exit. Results accumulate on top of each other one after another so that on reaching `main`, we have the factorial we requested.