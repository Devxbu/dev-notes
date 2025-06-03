
## Simple Assignment

A simple assignment replaces the value stored in the object designated by the left operand with the right operand. The value of the right operand is converted to the type of the assignment expression. Simple assignment has three components: the left operand, the assignment (=) operator and the right operand, as shown in the following example:

```c
int j = 21;
int j = 7;
i = j; // Simple assignment
```

In simple assignment the rvalue is converted to the type of lvalue and then stored in the object designated by the lvalue. 


```c
j = i + 12;
```

The expression i + 12 is not an lvalue, because there is no underlying object storing the result. Instead, i by itself is an lvalue that is automatically converted into an rvalue to be used as an operand to the addition operation.

An Lvalue must be a value that has a place in memory (variables etc). Lvalues can be written on both sides of the assignment. Rvalues are expressions that have no place in memory (numbers, letters, etc.) and can never be put on the left side.

```c
int i;
i = 5; // i is an lvalue, 5 is an rvalue
int j = i; // lvalues can appear on the right-hand side of an assignment.
7 = i; // error: rvalues can't appear on the left-hand side of an assignment 
```

The assignment 7 = i won't work, because the rvalue must always go on the right side of the operator.

## Evaluation

Evaluation is the process of executing an expression (using operators and operands) to produce a value. For example:

```c
int x = 3 + 4;
```

> 3 + 4 is evaluated -> the result is 7
> x is assigned 7

#### Evaluation stages
1. Operand is evaluated (numbers variables function calls etc)
2. Operators are applied (+, \*, -, ++, etc)
3. Handling side effects (e.g. assigning a value to a variable)

```c
int a = 2;
int b = 3;
int c = a + b * 4;
```

> `b * 4` → `12`, then `a + 12` → `14`

```c
int f() {
    printf(“Hello\n”);
    return 5;
}

int x = f() + 2;
```

> `f()` **evaluate** (side effect: “Hello” is printed), then `+ 2` is calculated.

#### Side Effect
> A side effect is when an expression not only produces a value but also changes the value of a variable.

```c
int a = 5;
int b = a++; // a++ is a side effect: first 5 turns, then a 6.
```

## Function Invocation

A function designator is an expression that has function type and is used invoke function. In the following function invocation, mas is the function designator:

```c 
int. x = 11;
int y = 21;
int max_of_and_y = max(x, y);
```

In an expression, a function designator is converted to pointer-to-function returning type at compile time. The value of each argument must be of a type that can be assigned to an object with (the unqualified version of) the type of its corresponding parameter.

## Increment and Decrement Operators

The increment (++) and decrement (--) operators increment and decrement a modifiable lvalue, respectively. Both are unary operators, because they take a single operand.

These operators can be used as either prefix operators, which come before the operand, or postfix operators which come after the operand. The prefix and postfix operators have different behaviors. A prefix increment performs the increment before returning the value, whereas a postfix increment returns the value and then performs the increment.

## Sizeof Operator

You can use the sizeof operator to find the size in bytes of its operand; specifically, it returns an unsigned integer of size_t type that represents size. The size_t type is defined in <stddef.h> as well as other header files.

```c 
int i;
size_t i_size = sizeof i; // the sizeof the object i
size_t int_size = sizeof(int); // the size of the type int
```

It is always safe to parenthesize the operand to sizeof, because parenthesizing an expression does not change the way the size of the operand is calculated.

## Unary + and - Operators

The unary + and 0 operators operate on a single operand of arithmetic type. The - operator returns the negative of its operand (25 -> -25). The unary + operator just returns the value. These operators exist primarily to express positive and negative numbers. 

>C has no negative integer constants; a values such as -25 is actually an rvalue of type int with the value 25 preceded by the unary - operator

## Logical Negation Operator

The result of unary logical negation (!) operator is as follow:

0 if the value of its operand is not 0
1 if the value of its operand is 0

The expression !E is equivalent to (0 == E). The logical negation operator is frequently used to check for null pointers; for example, !p is equivalent to (NULL == p).

## Bitwise Operators

We use bitwise operators to manipulate the bits of an object or any integer expression. Typically, they're used on objects that represent bitmaps: each bit indicates that something is "on" or "off". Bitwise ( |, &, ^, ~ ) operators treat the bits as a pure binary model without concern for the values represented by these bits. Bitmaps are best represented as unsigned integer types, as the sign bit can be better used as a value within the bitmap, and operations on the values are less prone to undefined behavior.

> 1. Bitwise AND Operator 
> The binary bitwise AND ( & ) operator returns the bitwise AND of two operands of integer type. 
> 
> 0 & 0 -> 0
> 1 & 0 -> 0
> 1 & 1 -> 1


>2. Bitwise Exclusive OR Operator (XOR)
>The bitwise exclusive OR ( ^ ) operator returns the bitwise exclusive OR of the operands of integer type
>
>0 ^ 0 -> 0
>1 ^ 1 -> 0
>1 ^ 0 -> 1

> 3. Bitwise Inclusive OR Operator 
> The bitwise inclusive OR ( | ) operator returns the bitwise inclusive OR of the operands of integer type.
> 
>  0 | 0 -> 0
>  1 | 0 -> 1
>  1 | 1 -> 1

> 4. Complement Operator
> The unary complement ( ~ ) operator works on a single operand of integer type and returns the bitwise complement of its operand: that is, a value in which each bit of the original value is flipped.
> 
> 0 -> 1
> 1 -> 0

## Shift Operators 

Shift operations shift the value of each bit of an operand of integer type by a specified number of positions. Shifting is commonly performed in system programming, where bit masks are common. 

```c
shift_expression << additive_expression // Number * (2 * shifted number)
```

```c
shift_expression >> additive_expression // Number / (2 * shifted number)
```

The shift expression is the value to be shifted and the additive expression is the number of bits by which to shift the value. The additive expression determines the number of bits by which to shift the value. For example, the result of E1 << E2 is the value of E1 left-shifted E2 bit positions: vacated bits are filled with zeros. If E1 has an unsigned type. In both kinds of shifts, the integer promotions are performed on the operands, each of which has the integer type. For signed integers, you must ensure that the number of bits shifted is not negative or greater than or equal to width of the promoted left operand. For unsigned integers.

## Logical Operators

The logical AND ( && ) operator and logical ( || ) OR operator are used primarily for logically joining two or more expressions of scalar type. You shouldn't use logical operators with bitmap operands, as they are intended primarily for Boolean logic. The && operator returns 1 if neither of its operands is equal to 0, and returns 0 otherwise. Logically this means that a && b is true only if both a is true and b is true. The || operator returns 1 if either of its operands is not equal to 0, and returns 0 otherwise. 

## Cast Operators

Cast (also known as type casts) explicitly converts a value of one type to a value of another type. There are two types of casting operations, the first is implicit casting and the second is explicit casting implicit casting is the automatic conversion of rounds, for example
```c
int i = 3;
float f = i;
```
There is implicit casting here, since the float type is larger than the int type, it is automatically cast.

To perform an implicit cast, an expression is preceded by a parenthesized type name, which converts the value of the expression to an unqualified version of the named type.

```c
// Syntax of explicit cast
(type) expression;

// Example
float pi = 3.14;
int i = (float) pi;
```

Unless the type name specifies a void type the name must be a qualified or unqualified scalar type. The operand must also have scalar type; a pointer type cannot be converted to any floating point type and vice versa. Casts are extremely powerful and must be used carefully. 
Casts may reinterpret the exsisting bits as a value of the specified type without changing bits

```c
intptr_t i = (intptr_t)some_pointer; // reinterpret bits as an integer 
```

Casts may also change these bits into whatever bits are needed to represent the original value in the resulting type

```c
int i = (int)some_float;  // change bits to an integer representation.
```

Casts can also disable diagnostics. For example, consider the following code snipped:

```c
char c;
// --- snip ---
while ((c = fgetc(in)) != EOF) {
// --- snip ---
}
```

Adding a cast to char disables the diagnostic without fixing the problem:

```c
char c;
while ((c = (char)fgetc(in)) != EOF) {
// --- snip ---
}
```

## Conditional Operators

It's like 1 line if else statement but returns a value as a function does. Unlike with an if else control flow block.

The conditional (?:) operator is the only C operator that takes three operands. It returns a result based on the condition. You can use the conditional operator like this:

```c
// Syntax of condition
result = condition ? valueReturnedIfTrue : valueReturnedIfFalse;

// Example
const int x = (a < b) ? b : a;
```

The conditional operator evaluates the first operand, called the condition. It evaluates either the second operand (valueReturnedIfTrue) if the condition is true, or the third operand (valueReturnedIfFalse) if the condition is false.

## \_Alignof Operator

The \_Alignof operator returns an integer constant representing the alignment requirements of the declared full object type of its operand. It does not evaluate the operand. When applied to an array type, it returns the alignment requirement of the element type. It is similar to sizeof, but they are fundamentally different things. sizeof gives the memory footprint of the variable being put into it, \_Alignof gives the number of bytes it should occupy in order to fit optimally in memory. Let's explain this with a few examples.

```c
// Syntax of the _Alignof
_Alignof (type)

// Example
_Alignof(char); // 1 byte
_Alignof(char); // 4 byte

typedef Struct {
        char c
        int i;
} Example;

sizeof(Example); // 5 byte
_Alignof(Example); // 8 byte
```

In the last example with struct, char takes up 1 byte and int 4 bytes why sizeof 5 alignof freezes 8 bytes. Because sizeof gives the total space it will occupy, while alignof tells you how many bytes it needs to spend to be optimally placed in memory.

## Comma

In C, we use commas in two different ways: as operators and as a way to separate items in a list (such as arguments to functions or declaration lists). The comma ( , ) operator is a way to evaluate one expression before another. First, the comma operator's removal operator evaluates to an empty expression.  

To use commas, we write the expressions we want to be made inside the parenthesis from left to right. 

```c
// Sytax of usage of comma
(expression_1, expression_2, expression_3);

// Example
int a = (1 + 2, 3 + 4); // 7
```

As you can see here, the condition to the right of the last comma is only assigned to the variable.
