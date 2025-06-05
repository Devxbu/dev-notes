## Expression Statement

We call expressions the code that ends with a semicolon, in which we perform operations, or just `;`.

```c
int x; // This is an expression that defines a variable
x = 5; // This is an expression that assigns a value to this variable
; // This is the void expression
```

## Compound Statements

Concatenated expressions or blocks group zero or more expressions together with curly braces. Inside these blocks we can put anything we have covered under this topic

```c
{
static int count = 4;
int c = 3;
count + c;
}
```

## Selection Statements

Selection expressions are expressions that allow us to perform an operation according to a condition.

### The if Statement

The if statement is used to execute the specified code if the condition written in it is satisfied. There are 2 types of if expressions, one is the expression that is given to us to be executed only when the condition is met and the other is the type that is used to call the expression even if the condition is not met

```c
// Syntax of type 1
if (expression) 
	substatement;

// Syntak of type 2
if (expression)
	substatement1;
else
	substatement2;
```

These if and else statements only allow us to call one expression below it, but if we use if and else statements and blocks together, we can call as many expressions as we want. (Most people write if and else statements using blocks to avoid mistakes.)

```c
if(age > 18){
	printf("He is adult: %d", age);
	adult = 1;
} else {
	printf("He is not an adult: %d", age);
	adult = 0
}
```

If we want to check multiple conditions separately, we use `else if (condition)`

```c
if (a = 5) printf("%d", a);
else if (a = 4) printf("%d", a);
else if (a = 3) printf("%d", a);
else if (a = 2) printf("%d", a);
else if (a = 1) printf("%d", a);
else printf("%d", a);
```


## Iteration Statements

The repetition of process causes the expressions written in it to be executed zero or more times. We call them loops. We have 3 types of loops (while, do-while, for).

## While Statement

While loop is an expression that executes the statements written in it until the condition is equal to 0. The syntax is as follows

```c
while(condition){
	expression;
}

// Example

int i = 5;
while(i <= 0){
	printf("%d. repetition: %d", 4 - i, i);
	i--;
} 
// 1. repetition: 5
// 2. repetition: 4
// 3. repetition: 3
// 4. repetition: 2
// 5. repetition: 1
```

It is possible to run a while loop an infinite number of times, so care must be taken when writing the condition. it must be ensured that the condition will be met after some time, and it must be remembered that the defined condition can be changed during the loop.

## The do-while Statement

The do-while loop works just like the while loop, a condition is written into it and it repeats the statements in the loop. The only difference is that in while the condition is first checked to see if the condition is met and then the values in the condition are executed if the condition is met. In do-while the expressions written in the do-while are executed once before the condition is met, then the condition is checked to see if the condition is met or not, and even if the condition is not met the expressions are called once. The syntax is as follows

```c
do{
	statement
} while(expression);

// Example

int i = 0;
do{
	printf("%d. repetition: %d", i, i);
	i++;
} while(i >= 5);

// 1. repetition: 1
// 2. repetition: 2
// 3. repetition: 3
// 4. repetition: 4
// 5. repetition: 5 LOOP HAS TO END HERE BUT EXPRESSIONS WORK 1 TIME MORE
// 6. repetition: 6
```

## The for Statement

The for statement works in the same way as while and do-while, by checking the condition in the statement and executing the written statements until the condition is not met. In other for statements, the variable to satisfy the condition is defined outside the statement and the increment and decrement operations are done in the body of the statement, but in the for statement everything is done in the section where the condition is written, below is an example syntax.

```c
for(clause; expression1; expression2){
	statement;
}

// Example

for (int i = 0; i <= 5; i++){
	printf("%d. repetition: %d", i, i);
}

// 1. repetition: 1
// 2. repetition: 2
// 3. repetition: 3
// 4. repetition: 4
// 5. repetition: 5
```

The for loop is popular among C programmers because it provides a convenient location for declaring and/or initializing the loop counter.

## The continue Statement

When we type `continue` inside a loop, it skips the following statements without executing them and the loop starts again. Let's examine the following example

```c
while(1){
	printf("Hey\n");
	continue;
	printf("Hello");
}

// Hey
// Hey
// Hey
// Hey
// ...
```

## The break Statement

When `break` is typed into a loop, the loop is terminated completely. Let's examine the following example.

```c
while(1){
	printf("Hey");
	break;
}

// Hey
```

## The return Statement

A return statement terminates execution of the current function and returns control to its caller. A function may have 0 or more return statements.

```c
int multiple(int x, int y){
	return x * y;
}
```