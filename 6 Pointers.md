# Pointers

A pointer is an object that refers (points) to some object or function, which simply means that a pointer is the memory address of some object or function.

<div style="margin: auto; width: fit-content;"><img src="6 Pointers.assets/ptr.png" alt="pointer" style="zoom:200%;" /></div>

<div style="font-size:14px; color: grey;">( Addresses here are shown as integers but in actual systems they will be in hexadecimal.) </div>

To create a pointer we prefix the ampersand symbol `&` to a variable or function name.

For example, suppose we have `int a = 10;` then using `&` with the variable `a` will give the address where the value `10` is stored. If we want to print the address using `printf`, we need to put the pointer format specifier `%p`. It prints the memory address in hexadecimal.

```c
#include <stdio.h>
void main() {
  int a = 10;
  printf("%p\n", &a); // prints the address where 10 is stored
}
```

Output

```
0x7ffdb01f5794
```

## Pointer Variables

Variables that store pointers are known as *pointer variables*. Their data type should be same as the object to which they are pointing.

<img src="6 Pointers.assets/ptr_variable.png" alt="ptr_variable" style="zoom:200%;" />

Being a variable, a pointer variable also occupies some memory space. Different implementations of the language allocate different sizes to pointer variables, which restricts the number of memory locations that you may use or access. For example, using an 8-bit addressing mechanism will allow us to access 2^8^ (=256) unique memory addresses and a 64-bit addressing mechanism will allow us to access 2^64^ (=18446744073709551616) unique addresses.

The memory size of a pointer is fixed within a computer or language that you are using, irrespective of the pointer's type. Therefore, a pointer of `int` type, a pointer of `float` type or any other pointer type will have the same  

### Declaration

Declaring a pointer variable is same as declaring any other variable, with just the small difference that variable names (declarators) must be prefixed with an asterisk symbol `*`.

Example: `float *p;`

Here we have declared a pointer variable `p` which can store the address of a `float` variable. 

The  type of a pointer variable must correspond with the type of the object it is going to point. For example if we want it to point to a `float` variable, then we have to define the pointer's type as `float` as well.

As another example, lets declare a pointer variable that will store a pointer to an integer object.  We'll call the pointer variable `p` and its type will be `int`. Also, we will initialise it to point to an `int` variable `a` having value `10`.

```c
#include <stdio.h>
void main() {
  int a = 10;
  int *p = &a;
  printf("%p\n", p);
}
```

In the line `int *p = &a;` above, the address of variable `a` is obtained using the `&` operator and then this address is stored in the pointer variable `p`.

- Formally, a pointer variable declaration has one the given forms:

  `specifiers-and-qualifiers` `*declarators-and-initializers` `;`, or

  `specifiers-and-qualifiers` `*` `declarators-and-initializers` `;`, or

  `specifiers-and-qualifiers*` `declarators-and-initializers` `;`

  <div style="font-size:14px; color: grey;">Note the positions of asterisk.</div>

- For multiple declarators: 

  `specifiers-and-qualifiers *declarator1, *declarator2, ...;` `;`

where,

- `specifiers-and-qualifiers` are a list of type specifiers, type qualifiers and storage-class specifiers. They specify the type of object that the pointer is mend to point.
- `declarators-and-initializers` are a comma-separated list of declarators (the variables we are declaring) and each of them must have an asterisk prefix. They may be accompanied by initializers.

### De-referencing

De-referencing helps us to access and modify the values kept at an address pointed to by a pointer. To de-reference a pointer, we use the de-reference operator `*`.

Suppose we have an integer variable `a` with value `10`,

`int a = 10;`

and we have stored the address of `a` in a pointer variable named `p`. 

`int *p = &a;`

Now how do we use the address stored in `p` to access the variable `a`? In other words we want to access the object `a` using its reference.

We do this by prefixing the de-reference operator `*` to the pointer variable `p`. We write `*p` which means the 'object at location `p`', that is `a`. Using `*p` we can do all operations that we could with `a`. 

As an example let's examine the following code. 

```c
#include <stdio.h>
void main() {
  int a = 10;
  int *p = &a;
  
  // access
  printf("%d\n", *p); // -> 10

  // modify
  *p = 20; // changes the value stored in a
  printf("%d\n", a); // -> 20
}
```

Here, we first print the value stored at the address pointed by `p` (which is `a`'s value), and then we change the value stored at that address by assigning `20` to de-referenced `p`. This changes the content of  `a` which we see by printing `a`'s value.

## Operators

We can use the following operators with pointers.

| Operator | Operator name                 | Example | Description                                                  |
| :------- | :---------------------------- | :------ | :----------------------------------------------------------- |
| `*`      | pointer de-reference          | `*a`    | de-reference the pointer **a** to access the object or function it refers to |
| `&`      | address of                    | `&a`    | create a pointer that refers to the object or function **a** |
| `->`     | member access through pointer | `a->b`  | access member **b** of struct or union pointed to by **a**   |

## Null pointers

A pointer referring to nothing is called a null pointer.

Pointer variables of every type have a special value known as null pointer value of that type. A pointer whose value is null does not point to an object or a function, and compares equal to all pointers of the same type whose value is also null.

To initialise a pointer variable to null or to assign the null value to an existing pointer, a null pointer constant (`NULL`, or any other integer constant with the value zero) may be used.

```c
char *ptr = NULL;
```

Null pointers can indicate the absence of an object or can be used to indicate other types of error conditions.

## Array Pointers

In C, there is a strong relationship between pointers and arrays. The name of an array is itself a pointer to its first (0th) element, so we can access, modify and traverse an array using pointer arithmetic. Basically, any operation that can be achieved by array sub-scripting can also be done with pointers. The pointer operation will in general be faster.

### Access and Modification

Pointers can be used to access and modify array members. For example, lets take the array `int a[] = {5, 10, 15, 20};`.

To *access* the 3rd array element using the sub-script notation we write `a[2]`. Same can be done using pointers by writing `*(a+2)`, which is a way of saying — de-reference the address that is 2 address units ahead of the base address `a`. 

The table below shows side by side comparison of accessing elements by subscripts and pointers.

| subscript notation |  pointer notation  | Value |
| :----------------: | :----------------: | :---: |
|       `a[0]`       | `*a` or `*(a + 0)` |   5   |
|       `a[1]`       |     `*(a + 1)`     |  10   |
|       `a[2]`       |     `*(a + 2)`     |  15   |
|       `a[3]`       |     `*(a + 3)`     |  20   |

Using the same access notation we can also *modify* the array values. For example, `*(a + 1) = 100` will be equivalent to `a[1] = 100`. After this operation `a` becomes `{5, 100, 15, 20}`.

### Traversal

If `p` is a pointer to some element of an array, then `p++` increments `p` to point to the next element, and `p += i` increments it to point `i` elements beyond where it currently does. We illustrate this in the following code.

```c
#include <stdio.h>
void main() 
{
  int a[] = {5, 10, 15, 20};
  
  // a pointer to the first element
  int *p = &a[0];

  p++; // increment
  printf("%d\n", *p); // -> 10

  p += 2; // hop
  printf("%d\n", *p); // -> 20
}
```

## Passing Array to Function

There are two ways of passing an array to a function.

- passing the array name
- passing a pointer to the array

## Pointers to String

In C, we cannot store strings in variables, but we can store a reference to the string in a pointer variable.

When we write something like this,

`char *s = "That's what she said!"`

we assign to variable `s` a pointer (reference) to the first element of the string `"That's what she said!"`.

Something similar happens implicitly in a function call with string arguments. Like in this function call,

`printf("Hello world\n");`

a pointer to the beginning of the character array is passed to `printf`.

However, there is a slight difference between a string literal reference and a character array declaration. Consider these two definitions:

```c
// a_msg is a character array
int a_msg[] = "That's what she said.";
```



```c
// P_msg is a string literal reference
int *p_msg = "That's what she said.";
```

`a_msg` is an array just big enough to hold the sequence of characters and `'\0'` that initialises it. Individual characters within the array may be changed and `a_msg` will always refer to the same storage.

```c
int a_msg[] = "That's what she said.";
a_msg[5] = 'z'; // -> "That'z what she said."
```

On the other hand, `p_msg` is a pointer, initialised to point to a string literal; the pointer may subsequently be modified to point elsewhere, but **the result is undefined if you try to modify the string constant using the pointer**.

```c
int *p_msg = "That's what she said.";
p_msg[5] = 'z'; // error: seg fault
```

## Structure Pointers

A structure pointer is a pointer pointing to a structure, meaning that it is the address of the beginning of a structure. We can obtain it using the 'address of' `&` operator on a structure variable and store it in a pointer variable of the same structure type.

```c
struct Thing {
    int member1, member2;
};

struct Thing t = { 10, 20 };
struct Thing *p = &t; // p refers to t
```

Note: A pointer to a struct can be cast to a pointer to its first member. Likewise, a pointer to the first member of a struct can be cast to a pointer to the enclosing struct. 

## Pointers within Structure

to-do