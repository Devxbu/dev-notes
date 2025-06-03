C was developed as a system programming language. System programming languages are designed for high performance and provide direct access to hardware resources, while still offering some high-level programming features.

Compiling
On a MacBook, you can compile your code using the following command:

```bash
cc test.c
```

If you want to specify the name of the output file, you can do so with:

```bash
cc -o name test.c
```

C defines two types of execution environments: freestanding and hosted. A freestanding environment typically does not include an operating system and is commonly used in embedded systems. It usually lacks access to standard input/output operations. A hosted environment, on the other hand, includes support for standard libraries and is generally used in applications that interact with an operating system.
