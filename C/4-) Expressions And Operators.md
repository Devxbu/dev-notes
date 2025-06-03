## Simple Assignment

A simple assignment replaces the value stored in the object designated by the left operand with the value of the right operand. The right operand is converted to the type of the assignment expression, if necessary. A simple assignment has three components: the left operand, the assignment (`=`) operator, and the right operand. For example:

```c
int i = 21; int j = 7; i = j; // Simple assignment
```

In a simple assignment, the rvalue (right-hand side) is converted to the type of the lvalue (left-hand side) and then stored in the object designated by the lvalue.

```c
j = i + 12;
```

In this expression, `i + 12` is not an lvalue because the result is not stored in a specific memory location. However, `i` by itself is an lvalue that is implicitly converted into an rvalue during evaluation of the addition.

An **lvalue** refers to an object that occupies identifiable memory (e.g., variables) and can appear on both sides of an assignment. An **rvalue** is a temporary value that does not refer to a memory location (e.g., literals like numbers or characters) and **cannot** be placed on the left-hand side of an assignment.

```c
int i; i = 5; // i is an lvalue, 5 is an rvalue int j = i; // lvalues can appear on the right-hand side too 7 = i; // error: rvalue on the left-hand side is not allowed
```

The expression `7 = i` is invalid because an rvalue cannot appear on the left side of an assignment.

---

## Evaluation

**Evaluation** is the process of executing an expression to produce a value. For example:

```c
int x = 3 + 4;
```

Here:

- `3 + 4` is evaluated, producing the result `7`
    
- `x` is then assigned the value `7`
    

### Stages of Evaluation

1. **Operands are evaluated** — such as numbers, variables, or function calls.
    
2. **Operators are applied** — like `+`, `*`, `-`, `++`, etc.
    
3. **Side effects are handled** — e.g., assigning values to variables or outputting to the screen.
    

Example:

```c
int a = 2; int b = 3; int c = a + b * 4;
```

- `b * 4` is evaluated first → `12`
    
- `a + 12` is then evaluated → `14`
    

```c
int f() {     printf("Hello\n");     return 5; }  int x = f() + 2;
```

- The function `f()` is evaluated first, printing `"Hello"`
    
- Then `5 + 2` is evaluated → `7` is assigned to `x`
    

### Side Effects

A **side effect** occurs when an expression not only yields a value but also changes the program's state.

```c
int a = 5; int b = a++; // Post-increment: b gets 5, then a becomes 6
```

---

## Function Invocation

A **function designator** is an expression that refers to a function and is used to call it. In the following example, `max` is the function designator:

```c
int x = 11; int y = 21; int max_of_x_and_y = max(x, y);
```

In an expression, the function name is automatically converted to a pointer to the function. Each argument passed to the function must be of a type that can be assigned to the corresponding parameter type of the function.

---

## Increment and Decrement Operators

The **increment** (`++`) and **decrement** (`--`) operators increase or decrease a modifiable lvalue by one, respectively. These are **unary operators**, meaning they operate on a single operand.

These operators can be used in **prefix** or **postfix** form:

- **Prefix (`++x`)**: The value is incremented before being used.
    
- **Postfix (`x++`)**: The original value is used, and then it is incremented.
    

---

## `sizeof` Operator

The `sizeof` operator returns the size (in bytes) of its operand. It yields a value of type `size_t`, which is defined in `<stddef.h>` and other headers.

```c
int i; size_t i_size = sizeof i;         // Size of variable i size_t int_size = sizeof(int);    // Size of type int
```

It's always safe to use parentheses around the operand, and doing so does not affect the result.

---

## Unary `+` and `-` Operators

The unary `+` and `-` operators apply to a single operand of arithmetic type.

- The `-` operator returns the **negation** of its operand (e.g., `25` becomes `-25`)
    
- The `+` operator simply returns the value unchanged
    

> C does not have negative constants; an expression like `-25` is parsed as a positive constant `25` followed by the unary minus operator.

## Logical Negation Operator

The unary **logical negation** operator (`!`) produces the following result:

- `1` if the operand is **zero**
    
- `0` if the operand is **non-zero**
    

In other words, `!E` is logically equivalent to `(0 == E)`.

This operator is often used to test conditions such as null pointers. For example:

```c
if (!p) { /* equivalent to if (p == NULL) */ }
```

---

## Bitwise Operators

**Bitwise operators** are used to manipulate individual bits of an integer value. They are especially useful for working with **bitmaps**, where each bit represents a flag — either "on" (`1`) or "off" (`0`). These operators work at the binary level and treat the data purely as sequences of bits.

> **Note:** It’s generally better to use **unsigned integer types** when working with bitwise operators to avoid issues with sign extension and undefined behavior.

### 1. Bitwise AND Operator (`&`)

The bitwise AND operator compares each bit of its operands and returns `1` only if both bits are `1`.

```c
0 & 0 → 0   1 & 0 → 0   1 & 1 → 1
```

### 2. Bitwise Exclusive OR (XOR) Operator (`^`)

The XOR operator returns `1` if **only one** of the corresponding bits is `1`. If both bits are the same, it returns `0`.

```c
0 ^ 0 → 0   1 ^ 1 → 0   1 ^ 0 → 1
```

### 3. Bitwise Inclusive OR Operator (`|`)

The OR operator returns `1` if **either** of the bits is `1`.

```c
0 | 0 → 0   1 | 0 → 1   1 | 1 → 1
```

### 4. Bitwise Complement Operator (`~`)

The complement operator inverts each bit of the operand: `0` becomes `1`, and `1` becomes `0`. This is a **unary** operator.

```c
~0 → 1   ~1 → 0
```

Note: In practice, `~` returns the two’s complement bitwise inversion, so `~x` is equivalent to `-(x + 1)` in signed integers.

---

## Shift Operators

**Shift operators** move the bits of an integer operand to the left or right by a specified number of positions. They are widely used in systems programming and bitmasking.

### Left Shift (`<<`)

Shifts all bits to the **left**, filling vacated bits with `0`. It effectively multiplies the number by a power of 2.

```c
x << n  // Equivalent to x * (2^n)
```

Example:

```c
int x = 3; int y = x << 2; // y = 12 (3 * 2^2)
```

### Right Shift (`>>`)

Shifts all bits to the **right**. For unsigned types, vacated bits are filled with `0`. For signed types, the behavior is implementation-defined (often arithmetic shift).

```c
x >> n  // Equivalent to x / (2^n)
```

Example:

```c
int x = 16; int y = x >> 2; // y = 4 (16 / 2^2)
```

### Notes on Shift Operations:

- The **left operand** must be of integer type.
    
- The **right operand** specifies the number of positions to shift.
    
- **Integer promotion** is applied before shifting.
    
- For **signed integers**, make sure the shift amount is not negative and does not exceed the bit width of the type.
    
- With **unsigned types**, shifts are more predictable and safe for bit manipulation.

## Logical Operators

The logical AND ( && ) operator and logical ( || ) OR operator are used primarily for logically joining two or more expressions of scalar type. You shouldn't use logical operators with bitmap operands, as they are intended primarily for Boolean logic. The && operator returns 1 if neither of its operands is equal to 0, and returns 0 otherwise. Logically this means that a && b is true only if both a is true and b is true. The || operator returns 1 if either of its operands is not equal to 0, and returns 0 otherwise. 

## Cast Operators

**Cast operators** explicitly convert a value from one type to another. There are two types of casting:

1. **Implicit casting** – automatic type conversion done by the compiler.
    
2. **Explicit casting** – manual type conversion done by the programmer.
    

### Implicit Cast

Implicit casting occurs when a value of a smaller or compatible type is automatically converted to a larger type.

```c
int i = 3; float f = i; // Implicit cast: int to float
```

Here, the `int` value is automatically promoted to a `float` because `float` has a larger range.

### Explicit Cast

An explicit cast is performed by placing the target type in parentheses before the expression:

```c
// Syntax: (type) expression  // Example: float pi = 3.14; int i = (int) pi; // Explicit cast: float to int
```

### Important Notes

- The target type (except `void`) must be a qualified or unqualified **scalar** type.
    
- The expression being cast must also be of scalar type.
    
- You **cannot** cast a pointer to a floating-point type or vice versa.
    

Explicit casts are powerful but should be used with caution. They can either:

- **Reinterpret** the existing bits:
    
```c
intptr_t i = (intptr_t)some_pointer; // Reinterpret pointer as integer
```
    
- **Convert** the value into a new representation:
    
```c
int i = (int)some_float; // Converts float to int
```
    

Casts can also **suppress compiler warnings**, which may lead to unintended behavior. For example:

```c
char c; while ((c = fgetc(in)) != EOF) { /* ... */ } // May cause logic error
```

Adding an explicit cast suppresses the warning, but not the underlying issue:

```c
char c; while ((c = (char)fgetc(in)) != EOF) { /* Still incorrect */ }
```

---

## Conditional Operator

The **conditional operator** (`?:`) is a compact alternative to the `if-else` statement. It evaluates a condition and returns one of two values based on the result.

### Syntax:

```c
condition ? value_if_true : value_if_false;
```

### Example:

```c
const int max = (a > b) ? a : b;
```

This line returns `a` if `a > b`, otherwise it returns `b`. The conditional operator is the only ternary operator in C, as it takes three operands.

---

## _Alignof Operator

The `_Alignof` operator returns the **alignment requirement** (in bytes) of a type. It does **not** evaluate the operand.

### Syntax:

```c
_Alignof(type)
```

### Example:

```c
_Alignof(char); // Usually 1 _Alignof(int);  // Usually 4  typedef struct {     char c;     int i; } Example;  sizeof(Example);    // Might return 8 due to padding _Alignof(Example);  // Might return 4 or 8 depending on the platform
```

Explanation:  
Even though the struct contains 1 `char` and 1 `int` (total 5 bytes logically), due to memory alignment, the compiler may insert padding to meet the alignment requirement of `int`, causing the size to increase (e.g., 8 bytes).

- `sizeof` gives the total memory used including padding.
    
- `_Alignof` shows the required alignment for optimal memory access.
    

---

## Comma Operator

In C, the **comma operator** (`,`) is used in two ways:

1. To **separate items** in a list (e.g., in function arguments or variable declarations).
    
2. As an **operator** to evaluate multiple expressions in sequence, where the result of the entire expression is the **rightmost** expression.
    

### Syntax:

```c
(expression1, expression2, ..., expressionN);
```

### Example:

```c
int a = (1 + 2, 3 + 4); // a = 7
```

Here:

- `1 + 2` is evaluated (result discarded),
    
- `3 + 4` is evaluated and its result (`7`) is assigned to `a`.
    

The **comma operator** ensures all expressions are evaluated in order from left to right, but only the final result is used.
