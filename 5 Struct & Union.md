#  Structure

In real world programming we have to deal with collections of data or structured information which have different attributes. For example, there are various items on an e-commerce website and each item has a name, price, brand, rating, comments etc. These attributes have different data types, for instance: name is string, price may be float or int. To group these data pieces into a collection or structure, C provides a data type called `struct`.

A `struct` clubs together small atomic objects (both basic and user-defined types) to create a big object. The small objects are then called members of that big `struct` object.

Formally, a `struct` is a user defined data type, which means that it's a custom type made on top of basic types and other user defined types. It consists of a sequence of members whose storage is allocated in an ordered sequence.

## Defining Structure

Structures allow full control over data organisation. In a structure definition, we define the layout for storing data in the structure.

We define a structure by using the `struct` keyword followed by a name (optional) and a parenthesised list of member declarations.

`struct name(optional) {  member-declaration-list };`

As an example, let's define a structure that represents an item on an e-commerce website.

```c
struct Item // name
{
    // members
    char name[50];
    char brand[50];
    float price;
    float rating;
    _Bool inStock;
};
```

Some points:

- The semicolon after the closing brace is necessary.
- A structure definition reserves no storage; it merely describes a template or shape of a structure.
- We can define structures anywhere in a program.
- Within a struct object, addresses of its elements increase in order in which the members were defined.

## Declaration of `struct` Variable

A standalone definition of a structure is just another data type. We can use it to create new objects.

Creating objects means creating entities of the given type that will occupy memory and hold values. To create struct objects we simply declare some variable with the given `struct` definition or name.

Syntax

`struct struct-name var1, var2, var3;`, or

`struct { ... }  var1, var2, var3;`

The following example shows declaration using the first syntax, where the struct has already been defined and we need only its name to declare new variables.

```c
struct Item iPhone_11, detergent, peanut_butter;
```

This is syntactically analogous to `int a, b, c;`. It declares `iPhone_11`, `detergent` and `peanut_butter` to be variables of the type `Item` and causes space to be set aside for them.

The second syntax shows us how we declare variables using a structure and define it at the same time. Here's an example.

```c
struct Item // name
{ 
    // members
    char name[50];
    char brand[50];
    float price;
    float rating;
    _Bool inStock;
} iPhone_11, detergent, peanut_butter;
```

Moreover, if we know that we won't need our custom type again, we can leave out the struct name and then define and declare together. So the above code can also be written as:

```c
struct 
{
    // members
    char name[50];
    char brand[50];
    float price;
    float rating;
    _Bool inStock;
} iPhone_11, detergent, peanut_butter;
```

## Initialisation

There are two ways of initialising structure variables.

1. during declaration

   A struct declaration can be followed by the assignment operator `=` and a parenthesised list of initializers in the order of the struct members, which will initialise them.

   ```c
   // Initialisation with declaration
   
   // at the time of definition
   struct Thing { 
       int attrib1;
       char attrib2;
       // ...
   } A = {100, 'F'}, 
     B = {10, 'A'};
   
   // OR separately
   struct Thing C = { 20, 'D'};
   ```

2. piece-wise

   In piece-wise initialisation, we use the member access operator `.` to initialise the members one by one.

   ```c
   
   struct Thing {
   	int attrib1;
       char attrib2;
       // ...
   } A; // declaration
   
   
   // initializing piece-wise
   A.attrib1 = 10;
   A.attrib2 = 'M';
   
   ```

## Assignment

The values of a structure variable can be assigned to another structure variable of the same type using the assignment operator. It is not necessary to copy structure members one by one.

In the following example, we declare two struct variables `A` and `B` and initialise the members of `A`. Then, by just using an assignment on the struct variables, we copy all of `A`'s data into `B`, which is verified by printing the members of B.

```c
struct {
    int property1;
    float property2;
} A, B;

A.property1 = 10;
A.property2 = 12.25;

// A gets copied into B
B = A;

printf("%d\n", B.property1); // -> 10
printf("%f\n", B.property2); // -> 12.25
```

## Structure Pointer

A structure pointer is a pointer pointing to a structure, meaning that it is the address of the beginning of a structure. We can obtain it using the 'address of' `&` operator on a structure variable and store it in a pointer variable of the same structure type.

```c
struct Thing {
    int member1, member2;
};

struct Thing t = { 10, 20 };
struct Thing *p = &t; // p refers to t
```

Note: A pointer to a struct can be cast to a pointer to its first member. Likewise, a pointer to the first member of a struct can be cast to a pointer to the enclosing struct. 

## Member Access

A member of a particular structure is accessed using the member access operator `.` in this way:

`structure-name.member-name;`

For example, if we wanted to access the member `price` of `detergent`, then we'd write `detergent.price`.

In case we have a pointer to a struct ( structure pointer) then we use `->` instead of `.` for member access.

`struct_ptr->member-name;`

Here's how we can access the member `brand` of `iPhone_11` via a pointer.

```c
// p is a pointer to struct object iPhone_11
struct Item *p = &iPhone_11;

// accessing member 'brand' using structure pointer 'p'
printf("Brand: %s\n", p->brand); // Apple
```

Using these expressions we can treat structure members like any ordinary variables. We can easily assign, access and modify the value in them.

Here's a program to demonstrate member access:

```c
#include <stdio.h>
#include <string.h>

struct Item
{
    char name[50];
    char brand[50];
    float price;
    float rating;
    _Bool inStock;
};

// prints item information
void show(struct Item item)
{	// a simple operation on a member
    char *msg = (item.inStock) ? "Available" : "Out of stock";
    
	// printing members
    printf(
        "-----------------\n"
        "Item name: %s\n"
        "Brand: %s\n"
        "Price: Rs. %0.2f\n"
        "Rating: %0.1f\n"
        "Availability: %s\n"
        "-----------------\n",
        item.name, item.brand, item.price, item.rating, msg);
}

void main()
{
    struct Item toy1;
    
    // assigning to members
    strcpy(toy1.name, "Toy Train");
    strcpy(toy1.brand, "Zephyr");
	toy1.price = 900.0;
    toy1.rating = 4.5;
    toy1.inStock = 1 // true;

        
    struct Item toy2 = {
        "Teddy Bear",
        "Cuddlies",
        350.5,
        4.0,
        0 // false
    };

    show(toy1);
    show(toy2);
}
```

```
-----------------
Item name: Toy Train
Brand: Zephyr
Price: Rs. 900.00
Rating: 4.5
Availability: Available
-----------------
-----------------
Item name: Teddy Bear
Brand: Cuddlies
Price: Rs. 350.50
Rating: 4.0
Availability: Out of stock
-----------------
```

## Nested Structure

A struct can have not only the basic types as its members but also other user defined types. This allows us to have another struct as a member of a struct.

For example we have a structure that represents points on a plane. There are three points named A, B and C. The structure representing the points has another structure within it representing the coordinates of the point.

```c
// structure representing a point in a plane
struct {
    char name[25]; // point name
    struct { 
        float x, y; // coordinates of the point
    } coords;
} A, B, C;
```

`struct { float x, y;}`, with which `coords` is declared, is a nested structure within the structure declaring the points. 

## Array of Structure

Suppose we have a `Student` structure representing a student.

```c
struct Student {
    char name[25];
    unsigned short roll_no;
    char course_code[2];
};
```

And we want to use this structure to store information of 100 students. 

Apparently, declaring 100 different variables of type `struct Student` isn't very practical, so instead, we can declare an array of type `struct Student` with size 100.

```c
struct Student students[100];
```

This is the same thing as declaring arrays of `int` or `char`, since `struct Student` is just another data type.

And now we can access each student one by one using indices and initialise their members.

Here's a program that demonstrates how to accept inputs in an array of structs.

```c
#include <stdio.h>

struct Student {
    char name[25];
    unsigned short roll_no;
    char course_code[2];
};

void main() {
    struct Student students[100];
    for (int i = 0; i < 100; ++i) {
        printf("Entry: %d\n", i);
        printf("Name: ");
        fgets(students[i].name, 25, stdin);
        printf("Roll No: ");
        scanf("%hu", &students[i].roll_no);
        printf("Course Code: ");
        scanf("%s", students[i].course_code);
        printf("\n");
    }  
}
```

## Structure as Function Argument

Like basic variables, a structure variable can also be passed to a function *by value*.

Structures wouldn't make much sense if we had to pass all their members separately. Thus the language allows us to pass and receive a structure as a whole like any ordinary variable.

When a function calls another function and passes a structure to it, a new copy of the structure is received in the parameter of the called function.

This example demonstrates how we pass a structure.

```c
struct Rectangle {
    int length;
    int bredth;
};

int area(struct Rectangle R) {
    return R.length * R.bredth;
}

void main() {
    struct Rectangle R = {15, 10};
    int a = area(R); // pass by value
    printf("Area = %d\n", a);
}
```

# Union

A union is a type consisting of a sequence of members whose storage overlaps. The value of at most one of the members can be stored in a union at any one time.

We define a union by using the `union` keyword followed by a name (optional) and a parenthesised list of member declarations.

`union name(optional) {  member-declaration-list }`

The union is only as big as necessary to hold its largest member. The other members are allocated in the same bytes as part of that largest member.

A pointer to a union can be cast to a pointer to each of its members. Likewise, a pointer to any member of a union can be cast to a pointer to the enclosing union.

If the member used to access the contents of a union is not the same as the member last used to store a value, the object representation of the value that was stored is reinterpreted as an object representation of the new type (this is known as *type punning*). If the size of the new type is larger than the size of the last-written type, the contents of the excess bytes are unspecified (and may be a trap representation).

```c
#include <stdio.h>
#include <string.h>
 
union Data {
   int i;
   float f;
   char str[20];
};
 
int main( ) {

   union Data data;        

   printf( "Memory size occupied by data : %d\n", sizeof(data));

   return 0;
}
```

```
Memory size occupied by data : 20
```

# Questions

- Differentiate between structure and union.

  -> Use points from the above explanations.

