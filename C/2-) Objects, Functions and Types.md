
When referenced an object can be interpreted as having a particular type. A variable is an example of an object represents. For example, an object with type int contains an integer value. The type is important because the collection of bits that represents one type object.

Functions are not objects but do have types. A function type is characterized by both its return type as well as the number and types of its parameters. 

The C language also has pointers, which can be thought of as an address location in memory where an object or function is stored. 

When you declare a variable, you assign it a type a provide it a name, of identifier, by which to reference the variable. Also you can generate variables in one line (but variables type has to be same)

```c
int x = 4;
float y = 4.5;
char z = "V"; 
```

C is a **Call-by-value language** which means that when you provide an argument to a function, the value of that argument is copied into a distinct variable for use within the function. You have to use pointer on swapping values in the functions. 

## Scopes

Objects, functions, macrons and other C language identifiers have scope that delimits the contiguous region where they can be accessed. C has four type of scope: file, block, function prototype and function.

The scope of an object or function identifier is determined by where it is declared. 

If the declaration is outside any block or parameter list, the identifier has **file scope**, meaning the scope is the entire text file in which appears as well as any files included after that point. 

If the declaration appears inside a block or within the list of parameter, it has **block scope** meaning that the identifier it declares is accessible only within the block

If the declaration appears within the list of parameter declarations a function prototype (not part of a function definition), the identifier has **function prototype scope**, which terminates at the end of the function declarator. Function scope is the area between the opening { of a function definition and its closing }. A label name is the only kind of identifier that has **function scope**. Labels are identifiers followed by a colon and identify a statement function to which control may be transferred.

If you declare the same identifier in both the inner and out scope, the identifier declared in the outer scope is hidden by the identifier within the inner scope, which takes precedence 

```c
#include <stdio.h>

int param = 4; // This is a file scope

void testFunction (param); // This is a function prototype scope

int main () {
	int param = 4; // This is a block scope
}
```

## Storage Duration

Objects have a storage duration that determines their lifetime. Altogether, four storage durations are available: automatic, static, thread and allocated.

***Scope and lifetime are entirely different concepts. Scope applies to identifiers, whereas lifetime applies to objects. The scope of an identifier is the code region where the object denoted by the identifier can be accessed by its name. The lifetime of an object is the time period for which the object exists***

Objects declared in file scope have static storage duration. The lifetime of these objects is the entire execution of the program, and their stored value is initialized prior to program startup. You can also declare a variable within a block scope to have static storage duration by using the storage class specifier static. Static object must be initialized with a constant value and not a variable.

Thread storage duration is used in concurrent programming. Its like a structures.

Allocated storage duration is enable you to static memory management. It generate  with malloc(), calloc(), realloc() ... functions.

```c
#include <stdio.h>

int x = 5; // Static variable

void testFunction () {
	int y = 3; // Automatic variable
	static int z = 4; // Static variable
}

int main () {
	int *list = (int *)malloc(size * sizeof(int)); // Allocated varaible
}
```

## Alignment 

Alignment is the rule of placing data at certain addresses in memory. The processor prefers to align certain data types at certain addresses in order to read the data faster.

For example:

char (1 byte) can stop at any address (1 byte alignment).
int (4 byte) must stop at addresses that are divisible by 4 (4 byte alignment).
double (8 byte) must stop at addresses that are divisible by 8 (8 byte alignment).
Purpose: To increase performance and allow the processor to read data in one go. In case of misalignments, the program will slow down, and may even crash on some processors!

Padding is the empty bytes added to ensure data alignment. These unnecessary bytes are added to ensure proper alignment in memory.

```c
struct Test {
    char a;    // 1 byte
    int b;     // 4 byte
    short c;   // 2 byte
};
```

the space occupied by this struct in memory changes as follows char 1 byte + 3 byte padding + int 4 byte + short 2 byte

 When used, pragma pack removes the paddings or reduces them by the number written.

```c
#pragma pack(1)

struct AlignmentTest {
    double d;  // 8 byte
    char c;    // 1 byte
    int i;     // 4 byte
};
```

Everything is 1 byte aligned, no padding! 

char + int  + double  = 13 byte

```c
#pragma pack(2)

struct AlignmentTest {
    double d;  // 8 byte
    char c;    // 1 byte
    int i;     // 4 byte
};
```

Everything is 2 byte aligned

char + 1 byte padding + int + double = 14 Byte

## Object Types

### Boolean Type
Objects declared as \_Bool can store only the values 0 and 1 but if you include the header <stdbool.h>, you can also spell this type as bool and assign it the values true (which expands to the integer constant) and false (which expands to the integer constant 0)

### Character Types
C language defines three character types: char, signed char and unsigned char. Each compiler implementation will define char to have same alignment. The char type is commonly used to represent character data in C language programs. You can represent the characters of a large character set as wide characters by using wchar_t type which generally takes more space than a basic character. Typically, implementations choose 16 or 32 bits to represent a wide character. The C Standard Library provides functions that support both narrow and wide character types.

### Integer Types
Signed integer types can be used to represent negative numbers, positive numbers, and zero. The signed integer types include *signed char, short int, int, int, long int, and long long int*. For each signed integer type, there is a corresponding unsigned integer type that uses the same amount of storage: *unsigned char, unsigned short int, unsigned int, unsigned long int, and unsigned long long int* The unsigned types can be used to represent only positive numbers and zero. 

### Enum Types
An enumeration, or enum, allows you to define a type that assigns names to integer values in cases with an enumerable set of constant values.

```c
enum day {sun, mon, tue, wed, thu, fri, sat};
enum cardinal_points {north = 0, east = 90, south = 180, west = 270};
```

If you don't specify a value to the first enumerator with the = operator, the value of its enumeration constant is 0, and each subsequent enumerator without an = adds 1 to the value of the previous enumeration constant.

### Void Types
The keyword void means "cannot hold any value." For example, you can use it to indicate that a function doesn't return a value, pr as the sole parameter of a function to indicate that the function takes no arguments. On the other hand, the derived type void * means that the pointer can reference any object.

### Function Types 
Function types are derived types. In this case, the type is derived from the return type and the number and types of its parameters. The return type of a function cannot be an array type. When you declare a function, you use the function declarator to specify the name of the function and the return type. 

### Derived Types 
Derived types are types that are constructed from other types. These include pointers. arrays, type definitions, structures , and unions, all of which we'll cover here.

#### Pointer Types [[!-) Pointers]] 
A pointer type is derived from the function or object type that it points to, called the referenced type. A pointer provides a reference to an entity of the referenced type.

```c
int *ip;
char *cp;
void *vp;
```

The following three declarations declare a pointer to int, a pointer to char and a pointer to void.

You can use the & operator to take the address of an object or function. After that using * operator define address in the pointer.

```c
int i = 8;
int *ip = &i;
```

We declare the variable ip as a pointer to int and assign it the address of i.

### Arrays
An array is a contiguously allocated sequence of objects that all have the same element type. Array types are characterized by their element type and the number of elements in the array. Here is a example of the array definition

```c
int numbers[11];
float *afp[17];
```

Using square brackets (\[]) for identify element of an array. For example the following contrived code snippet creates the string "0123456789" to demonstrate how to assing values to the elements of an array:

```c
char str[11];
for (unsigned int i = 0; i < 10; ++i){
	str[i] = '0' + i;
}
str[10] = '\0';
```

The first line declares an array of char with a bound of 11. This allocate s sufficient storage to create a string with 10 characters plus a null character.

### Structures
A  structure type contains sequentially allocated member objects. Each object has its own name and may have distinct type unlike arrays, which must all be of the same type. Here is a example for a defining structure.

```c
struct sigrecord {
	int signum;
	char signame[20];
	char sigdesc[100];
} sigline, *sigline_p;
```

Once you have defined a structure, you'll likely want to reference its members. You reference members of an object of the structure type by using structure member (.) operator. If you have a pointer to a structure, you can reference its members with the structure pointer (->) operator

### Unions 
Union types are similar to structures, except that the memory used by the member objects overlaps. Unions can contain an object of one type at one time, and an object of a different type at a different time, butt never both object at the same time, and are primarily used to save memory. Here is a example.

```c
union {
	stuct {
		int type;
	} n;
	stuct {
		int type;
		int intnode;
	} ni;
}
```

As with structures, you can access union members via the . operator. Using a pointer to a union, you can reference its members with the -> operator.

### Tags
Tags are a special naming mechanism for structs, unions and  enums. For example, the identifier s appearing in the following structure is a tag.

```c
struct s {
	// --- snip ---
}
```

By itself a tag is not a type name and cannot be used to declare a variable. Instead you must declare variables of this types of follow.

```c
struct s v; // Instence of struct s
sturct s *p; // Pointer to struct s

enum day {sun, mon, tue, wed, thu, fri, sat};
day today; // Error
enum day tomorrow; // Ok
```

But we can use only tags when we used the typedef

```c
typedef struct {
	char name[50];
	int age;
} Person; // Now we can access this struct with Person tag
```

### Type Qualifiers
Types can be qualified by using one or more of the following qualifiers: const, volatile and restrict. Each of these qualifiers changes behaviors when accessing objects of the qualified type.

	CONST
	Objects declared with the const qualifier are not modifiable. In particular, 
	they're not assignable but can have constant initializers. This means object 
	with const-qualified types can be placed in read-only memory by they 
	compiler, and any attempt to write to them will result in a runtime error.

	VOLATILE
	Objects of voliatile-qualified types serve a special purpopse. Static 
	volatile-qualified objects are used to model memory-mapped input/output 
	(I/O) ports, and static constant volatile-qualified objects model memory-
	mapped input ports such as a real-time clock. The values stored in these 
	object may change without the knowledge of the compiler. Also volatile-
	qualified types are used for communucations with signal handlers and with 
	setjmp/longjmp. Volatile-qualified types in C should not be used for 
	synchronization between threads.

	RESTRICT
	A restrict-qualified pointe is used to protomote optimization. Objects 
	indirectyly accessed through a pointer frequantly cannot be fully optimized 
	because of potential aliasing, which occurs when more than one pointer 
	refers to the same object.