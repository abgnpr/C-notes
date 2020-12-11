# Memory Allocation

Memory allocation is the process of reserving a portion of computer memory for the execution of programs and keeping associated data. 

Memory allocation is also referred to as memory management because we manually acquire memory and then free it on the basis of our needs. This helps to optimise its usage.

The figure below shows different sections of a computer memory. We'll discuss how a program allocates and manages different types of objects in each section.

<img src="7 DMA.assets/memory-allocation-in-c.webp" id="alloc-overview" alt="dynamic memory allocation in c" style="zoom: 80%;" />

## Types of Memory Allocation

There are three different types of memory allocation:

- Static
- Automatic
- Dynamic

The C language supports the first two kinds of memory allocation (static and automatic) through variables. The third kind, *dynamic allocation*, is not supported by C variables but is available via GNU C Library functions and is mend to be used with the help of pointers.

We'll see dynamic memory allocation in detail along with the library functions that are used to achieve it.

### Static allocation 

Static allocation happens when you declare a static or global variable. Each static or global variable defines one block of space, of a fixed size. The space is allocated once, when your program is started (part of the exec operation), and is never freed.

Statically allocated objects get their memory in the permanent storage area. ([See image](#alloc-overview))

### Automatic allocation

Automatic allocation happens when you declare an automatic variable, such as a function argument or a local variable. The space for an automatic variable is allocated when the compound statement containing the declaration is entered, and is freed when that compound statement is exited.

Automatically allocated objects are stored on the stack. ([See image](#alloc-overview))

### Dynamic Allocation

*Dynamic memory allocation* is a technique in which programs determine as they are running where to store some information. In other words, the process of allocating memory at run time is known as **dynamic memory allocation**.

#### Need

Dynamic allocation is done when the amount of memory we need or the duration for which we need it depends on factors that are not known before the program runs.

- For example, we may need a block to store a line read from an input file; since there is no limit to how long a line can be, we must allocate the memory dynamically and make it dynamically larger as we read more of the line.

- Or, we may need a block for each record or each definition in the input data; since we can’t know in advance how many there will be, we must allocate a new block for each record or definition as we read it.

#### How Dynamic Allocation is done

- When we use dynamic allocation, the program explicitly requests the allocation of a block of memory via a system call (which is generally via a GNU C Library function call). 

- We have the library functions `malloc` and `calloc` which can be called along with size as argument to allocate the space we require. 

- The region of memory used for dynamic memory allocation is the heap ([See image](#alloc-overview)). Heap is the memory space between the permanent storage area and the stack and its size keeps changing.

- If we want to free previously allocated space, we use the library function `free` and if we want to extend or shrink previously allocated space we use `realloc`.

- We can allocate and de-allocate space whenever we want and as often as we want.

- The only way to refer to dynamically allocated space is through a pointer. For example, if we want to dynamically allocate some space to hold a `struct Foobar` object, we can't simply declare a `struct Foobar` variable and store the dynamically allocated content in it. We need to declare a `struct foobar` pointer variable (`struct foobar *`) and then we can assign to it the address of the allocated space:

  ```c
  
  struct foobar *ptr = (struct foobar *) malloc (sizeof (struct foobar));
  ```



Dynamic allocation is not supported by C variables; there is no storage class “dynamic”, and there can never be a C variable whose value is stored in dynamically allocated space.

Because it is less convenient, and requires more computation time, programmers use dynamic allocation only when neither static nor automatic allocation will serve.



#### Reasons to Use, and Advantages

We use dynamic memory allocation in the following cases.

1. When we do not know how much amount of memory would be needed for the program beforehand.
2. When we want data structures without any upper limit of memory space.
3. When you want to use your memory space more efficiently. Example: If you have allocated memory space for a 1-D array as array[20] and you end up using only 10 memory spaces then the remaining 10 memory spaces would be wasted and this wasted memory cannot even be utilised by other program variables.
4. Dynamically created lists insertions and deletions can be done very easily just by the manipulation of addresses whereas in case of statically allocated memory insertions and deletions lead to more movements and wastage of memory.
5. When you want to use the concept of structures and linked list in programming, dynamic memory allocation is a must



## Dynamic Memory Management Functions

Library routines known as **memory management functions** are used for allocating and freeing memory during execution of a program.

### `malloc()`

Allocates a fixed number of bytes of uninitialised storage.

Defined in: `<stdlib.h>`

Usage syntax: `malloc(size);`

Prototype: `void* malloc( size_t size );`

where, `size` is the number of bytes to be allocated.

If allocation succeeds, returns the pointer to the beginning of newly allocated memory. On failure, returns a null pointer.

If `size` is zero, the behavior is implementation defined (null pointer may be returned, or some non-null pointer may be returned that may not be used to access storage, but has to be passed to `free`).

When done using the allocated space, the returned pointer must be de-allocated with `free()` or `realloc()`, to avoid a memory leak.

Example:

```c
#include <stdio.h>   
#include <stdlib.h> 
 
int main(void) 
{
    int *p1 = malloc(4*sizeof(int));  // allocates enough for an array of 4 int
    int *p2 = malloc(sizeof(int[4])); // same, naming the type directly
    int *p3 = malloc(4*sizeof *p3);   // same, without repeating the type name
 
    if(p1) {
        for(int n=0; n<4; ++n) // populate the array
            p1[n] = n*n;
        for(int n=0; n<4; ++n) // print it back out
            printf("p1[%d] == %d\n", n, p1[n]);
    }
 
    free(p1);
    free(p2);
    free(p3);
}
```

Output

```
p1[0] == 0
p1[1] == 1
p1[2] == 4
p1[3] == 9
```



### `calloc()`

Allocates memory for an array of a given fixed number of objects of a given fixed size, and initialises all bytes in the allocated storage to zero.

Defined in: `<stdlib.h>`

Usage syntax: `calloc(num, size)`;

Prototype: `void* calloc( size_t num, size_t size );`

where, `num` is the number of objects to be allocated and `size` is the size of each object.

If allocation succeeds, returns the pointer to the beginning of newly allocated memory. On failure, returns a null pointer.

If `size` is zero, the behavior is implementation defined (null pointer may be returned, or some non-null pointer may be returned that may not be used to access storage).

Note: Due to the alignment requirements, the number of allocated bytes is not necessarily equal to `num*size`.

Example:

```c
#include <stdio.h>
#include <stdlib.h>
 
int main(void)
{
    int *p1 = calloc(4, sizeof(int));    // allocate and zero out an array of 4 int
    int *p2 = calloc(1, sizeof(int[4])); // same, naming the array type directly
    int *p3 = calloc(4, sizeof *p3);     // same, without repeating the type name
 
    if(p2) {
        for(int n=0; n<4; ++n) // print the array
            printf("p2[%d] == %d\n", n, p2[n]);
    }
 
    free(p1);
    free(p2);
    free(p3);
}
```

Output

```
p2[0] == 0
p2[1] == 0
p2[2] == 0
p2[3] == 0
```



### `realloc()`

Reallocates a given area of memory which has been previously allocated by `malloc()`, `calloc()` or `realloc()` and not yet freed with a call to `free` or `realloc`. 

Defined in: `<stdlib.h>`

Usage syntax: `realloc( ptr, new_size );`;

Prototype: `void *realloc( void *ptr, size_t new_size );`

where, `ptr` is the pointer to the memory area to be reallocated and `new_size` is new size of the array in bytes.

The results are undefined if the given area has already been freed.

The reallocation is done by either:

- expanding or contracting the existing area pointed to by `ptr`, if possible. The contents of the area remain unchanged up to the lesser of the new and old sizes. If the area is expanded, the contents of the new part of the array are undefined.
- or allocating a new memory block of size `new_size` bytes, copying memory area with size equal the lesser of the new and the old sizes, and freeing the old block.

If there is not enough memory, the old memory block is not freed and null pointer is returned.

If `ptr` is `NULL`, the behavior is the same as calling `malloc`(`new_size`).

If `new_size` is zero, the behavior is implementation defined (null pointer may be returned (in which case the old memory block may or may not be freed), or some non-null pointer may be returned that may not be used to access storage).

Example:

```c
#include <stdio.h>
#include <stdlib.h>
 
int main(void)
{
    int *pa = malloc(10 * sizeof *pa); // allocate an array of 10 int
    if(pa) {
        printf("%zu bytes allocated. Storing ints: ", 10*sizeof(int));
        for(int n = 0; n < 10; ++n)
            printf("%d ", pa[n] = n);
    }
 
    int *pb = realloc(pa, 1000000 * sizeof *pb); // reallocate array to a larger size
    if(pb) {
        printf("\n%zu bytes allocated, first 10 ints are: ", 1000000*sizeof(int));
        for(int n = 0; n < 10; ++n)
            printf("%d ", pb[n]); // show the array
        free(pb);
    } else { // if realloc failed, the original pointer needs to be freed
        free(pa);
    }
}
```

Output

```
40 bytes allocated. Storing ints: 0 1 2 3 4 5 6 7 8 9
4000000 bytes allocated, first 10 ints are: 0 1 2 3 4 5 6 7 8 9
```



### `free()`

De-allocates the space previously allocated by `malloc()`, `calloc()` or `realloc()`.

Defined in: `<stdlib.h>`

Usage syntax: `free( ptr );`;

Prototype: `void free( void *ptr );`

where, `ptr` is a pointer to the memory to de-allocate. If `ptr` is a null pointer, the function does nothing.

Return value: (none).

Whether allocation succeeds or not, the pointer returned by an allocation function can be passed to `free()`.

The behaviour is undefined in the following cases:

- If the value of `ptr` does not equal a value returned earlier by `malloc()`, `calloc()`, or `realloc()`.
- If the memory area referred to by `ptr` has already been de-allocated, that is, `free()` or `realloc()` has already been called with `ptr` as the argument and no calls to `malloc()`, `calloc()` or `realloc()` resulted in a pointer equal to `ptr` afterwards.
- If after `free()` returns, an access is made through the pointer `ptr` (unless another allocation function happened to result in a pointer value equal to `ptr`).

Example:

```c
#include <stdlib.h>
 
int main(void)
{
    int *p1 = malloc(10*sizeof *p1);
    free(p1); // every allocated pointer must be freed
 
    int *p2 = calloc(10, sizeof *p2);
    int *p3 = realloc(p2, 1000*sizeof *p3);
    if(p3) // p3 not null means p2 was freed by realloc
       free(p3);
    else // p3 null means p2 was not freed
       free(p2);
}
```

## Appendix

### `sizeof()` operator

Queries size of the object or type.

Used when actual size of the object must be known.

It's a keyword.

Usage syntax:

1. `sizeof( type )`
2. `sizeof expression`

Both versions return a value of type `size_t`.

- 1 returns the size, in bytes, of the object representation of *type*

- 2 returns the size, in bytes, of the object representation of the type of *expression*. No implicit conversions are applied to *expression*.

```c
#include <stdio.h>
 
int main(void)
{
    short x;
    // type argument:
    printf("sizeof(float)          = %zu\n", sizeof(float));
    printf("sizeof(void(*)(void))  = %zu\n", sizeof(void(*)(void)));
    printf("sizeof(char[10])       = %zu\n", sizeof(char[10]));
//  printf("sizeof(void(void))     = %zu\n", sizeof(void(void))); // Error: function type
//  printf("sizeof(char[])         = %zu\n", sizeof(char[])); // Error: incomplete type
 
    // expression argument:
    printf("sizeof 'a'             = %zu\n", sizeof 'a'); // type of 'a' is int
//  printf("sizeof main            = %zu\n", sizeof main); // Error: Function type
    printf("sizeof &main           = %zu\n", sizeof &main);
    printf("sizeof \"hello\"         = %zu\n", sizeof "hello"); // type is char[6]
    printf("sizeof x               = %zu\n", sizeof x);   // type of x is short
    printf("sizeof (x+1)           = %zu\n", sizeof(x+1)); // type of x+1 is int
}
```

```
sizeof(float)          = 4
sizeof(void(*)(void))  = 8
sizeof(char[10])       = 10
sizeof 'a'             = 4
sizeof &main           = 8
sizeof "hello"         = 6
sizeof x               = 2
sizeof (x+1)           = 4
```

