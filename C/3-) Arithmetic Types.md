
Most operators in C operate on arithmetic types. Because C is a system-level language, performing arithmetic operations correctly can be difficult -resulting in frequent defects.

## Integers
Integers represents a finite range of integer. Signed integer types represent values that can be negative, zero or positive; unsigned integers represent values that can be only zero or positive.  

All integer types except *char, signed char and unsigned char* may contain unused bits, called padding, that allow implementations to accommodate hardware quirks (such as skipping over a sign bit in the middle of a multiple-word representation) or optimally align with a target architecture.

The <limits.h> header file provides the minimum and maximum representable values for the various integer types. A representable value is on that can be represented in the number of bits available to an object of a particular type. Values cannot be represented will be diagnosed by the compiler or converted to a representable but different value. Compiler writers provide the correct minimum, maximum and width values for their implementations. 

Unless explicitly declared as unsigned, integer types are assumed to be signed. 

```c
unsigned int ui; // unsigned is required
unsigned u; // int can be ommited
```

## Unsigned Integers
Unsigned integers have range that start at 0, and their upper bound is greater than that of the corresponding signed integer type. Unsigned integers are frequently used for counting items that may have large, nonnegative quantities.

## Wraparound
Wraparound occurs when you perform arithmetic operations that result in values too small (less than 0) or too large (greater than 2^N - 1) to be represented as a particular unsigned integer type. In this case value is reduced modulo the number that is one greater than the largest value that can be represented in the resulting type. Wraparound is well-defined behavior in the C language. Whether it is a defect in your code depends on the context. If you are counting something and the value wraps, it is likely to be an error. 

## Signed Integers
Each unsigned integer type (excluding \_Bool) has a corresponding signed integer type that occupies the same amount of storage. We use signed integers to represent negative, zero, and positive values, the range of which depends on the number of bits allocated to the type and the representation. 

## Integer Constants 
Integer constants are constants we use to introduce particular integer values into a program. C has three kind of integer constants that use different number systems: decimal constants (10), octal constants (8), and hexadecimal constants (16).

Decimal constants always begin with a nonzero digit.

```c
unsigned int ui = 71;
int si;
si = -12;
```

If a constant starts with a 0, optionally followed by digits 0 through 7 it is an octal constant.

```c
int agent = 007;
int premissions = 0777;
```

You can also create a hexadecimal constant by prefixing a sequence of decimal digits and the letters a (or A) through f (of F) with 0x or 0X

```c
int burger = 0xDEADBEEF;
```

Use hexadecimal constants when the constant you are introducing is meant to represent a bit pattern more than a particular value. 

You can also append a suffix to your constant to specify its type. The suffixes are U for unsigned, L for signed long, and LL for long long. These can be combined.

```c
unsigned int ui = 71U;
signed long int sli = 838484958L;
unsigned long long int ui = 82390844878484ULL;
```

If we don't use a suffix, and the integer constant isn't of the required type, it may be implicitly converted.

## 1. Floating-Point Types

Floating-point numbers are used to represent real numbers, i.e., numbers that have a fractional part. In C, these numbers can be represented using three different data types:

### 1.1. `float`
- The **`float`** type is typically represented with 32 bits (4 bytes).
- **Characteristics:**
  - Provides approximately **7 decimal digits of precision**.
  - Represents **single precision** floating-point numbers.

### 1.2. `double`
- The **`double`** type is typically represented with 64 bits (8 bytes).
- **Characteristics:**
  - Provides approximately **15-16 decimal digits of precision**.
  - Represents **double precision** floating-point numbers.

### 1.3. `long double`
- The **`long double`** type can be represented with 80, 128, or more bits, depending on the system.
- **Characteristics:**
  - Provides higher precision than `double` but may use more memory.
  - The exact size varies between platforms.

---

## 2. Floating-Point Arithmetic

Floating-point arithmetic is used when performing calculations on numbers with a fractional part. Due to the finite representation of floating-point numbers, there are some inherent limitations and issues with floating-point arithmetic:

### 2.1. General Structure of Floating-Point Representation
Floating-point numbers are represented in scientific notation as:

```
(+/-) mantissa × base^exponent
```

For example, the number **`3.14`** can be represented as:

```
3.14 = 0.314 × 10^1
```

### 2.2. Common Floating-Point Arithmetic Issues
Some common issues encountered when working with floating-point arithmetic include:

- **Rounding Errors:** Not all decimal numbers can be exactly represented, leading to rounding errors.
- **Overflow and Underflow:** Operations on very large or very small numbers may result in overflow (values too large to represent) or underflow (values too small to represent).

### 2.3. Example:

```c
#include <stdio.h>

int main() {
    float a = 1.0f;
    float b = 1.0f / 3.0f;
    float c = a + b;
    
    printf("a = %.7f\n", a);  // a = 1.0000000
    printf("b = %.7f\n", b);  // b ≈ 0.3333333
    printf("c = %.7f\n", c);  // c ≈ 1.3333333
    return 0;
}
```

In this example, the `float` type introduces small errors due to its limited precision.

## 3. Floating-Point Values

Floating-point values are numbers represented using the `float`, `double`, or `long double` types. These values are used when performing calculations with real numbers.

### 3.1. Range of Floating-Point Types:

Each floating-point type has a specific range of values it can represent:

- **`float`:**
    
    - Can represent values approximately from **1.4 × 10⁻⁴⁵** to **3.4 × 10³⁸**.
        
    - **Minimum Positive Value:** `1.175494351e-38F`
        
    - **Maximum Value:** `3.402823466e+38F`
        
- **`double`:**
    
    - Can represent values approximately from **5.0 × 10⁻³²** to **1.7 × 10³⁰**.
        
    - **Minimum Positive Value:** `2.2250738585072014e-308`
        
    - **Maximum Value:** `1.7976931348623157e+308`
        
- **`long double`:**
    
    - The range of `long double` varies by platform but generally offers a larger range than `double`.
        

### 3.2. Limitations of Floating-Point Representation:

Since floating-point numbers are represented with finite precision, there can be **overflow** (when the value exceeds the maximum representable value) or **underflow** (when the value is too small to be represented).

## 4. Floating Constants

Floating constants are numeric constants that represent floating-point values in C. These constants can be of type `float`, `double`, or `long double`.

### 4.1. Writing Floating Constants

Floating constants can be written in either **decimal** or **scientific** notation.

- **Decimal Notation:**

```c
float f = 3.14f;  // 'f' suffix indicates a float
double d = 3.14;  // default is double
```

- Scientific Notation:

```c
float f = 1.23e4f;  // 1.23 * 10^4
double d = 2.718e-3; // 2.718 * 10^-3
```

### 4.2. `f`, `l` and `F`, `L` Suffixes

- **`f` or `F`**: Indicates that the constant is of type `float`.
    
- **`l` or `L`**: Indicates that the constant is of type `long double`.
    

### 4.3. Example:

```c
#include <stdio.h>

int main() {
    float f = 3.14f;
    double d = 3.14159265359;
    long double ld = 3.141592653589793238L;

    printf("float: %.2f\n", f);
    printf("double: %.15f\n", d);
    printf("long double: %.20Lf\n", ld);

    return 0;
}
```


## Arithmetic Conversion

In C, we use type casting when we want to convert one data type to another data type. There are 2 types of type casting: Implicit Type Casting and Explicit Type Casting

### Implicit Type Casting

In some cases the C compiler **automatically** performs a type conversion. This usually happens when moving from “smaller species to larger species”.

```c 
int i = 10;
float f = i; // int -> float (automatic)
printf(“%f\n”, f); // 10.000000
```

Here the int data type is switched to the float data type. There is no data loss because float is larger than int.

### Explicit Type Casting

A type conversion done by the programmer, explicitly specified in parentheses.

```
(type_name) value
```

In this way it is possible to manually make conversions between tours.

```c
float f = 3.14;
int i = (int)f; // float -> int, decimal part disappears
printf(“%d\n”, i); // 3
```

#### Why use type casting?

- To resolve species mismatches
    
- To trade in the target type
    
- For hardware-level bit manipulation
    
- To convert `void *` pointers to usable types

#### Things to watch out for

Data loss may occur

```c
float f = 1234.5678;
int i = (int)f; // the decimal part disappears
```

Signed/Unsigned conversions may experience overflow

```c
unsigned int u = (unsigned int)(-10); // becomes wraparound
printf(“%u\n”, u); // 4294967286 (on 32-bit system)
```
### Pointer Type Casting

##### Void* conversion

```c
void *vp;
int x = 5;
vp = &x;

printf(“%d\n”, *(int *)vp); // convert void pointer to int pointer
```

##### Type punning (common in C, but be careful)

```c
float f = 3.14;
int *ip = (int *)&f; // interpret float as int
printf(“%d\n”, *ip); // treat bit-level float as int
```


## Integer Conversation Rank

In C, when **different integer types** (`char`, `int`, `long`, `unsigned int` etc.) come together, **rank** is the **priority ranking used to decide **which one to convert to which one**.

The **rank** determines the answer to questions like _“char to int, int to long?”_.

In C, the rank order from lowest to highest (for standard types) is as follows:

| Sequence | Type |
| ---- | -------------------------------------- |
| 1 | `_Bool` |
| 2 | `char`, `signed char`, `unsigned char` |
| 3 | `short`, `unsigned short` |
| 4 | `int`, `unsigned int` |
| 5 | `long`, `unsigned long` |
| 6 | `long long`, `unsigned long long long` |

## Why Does This System Exist?

Because the C compiler thinks:

	“I need to process two types together. If I convert the small type to a 
	large type, the data 
	no loss. But if I change the large type to small, I might lose data. Then 
	I'll lose Let me turn the small into a big one!”

```c
char c = 100;
int i = 20;
int result = c + i; // char → int, operation becomes int + int
```

Where `char` is of lower rank than `int` → **automatically converts to `int`.

```c
int i = -1;
unsigned int u = 1;
if (i < u) {
    printf(“i is less than u\n”);
}
```

But beware!

- Here `int` and `unsigned int` can be **same width** (e.g. 32-bit).
    
- However, `unsigned int` has a **higher rank** than `int`.
    
- Therefore `i` is converted to `unsigned int`: `-1` → `4294967295`!

```nginx
if (4294967295 < 1) ➜ false!
```

And nothing is written on the screen!
