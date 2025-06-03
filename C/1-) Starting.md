C was developed as a system programming language. System languages are designed for performance and ease of access to the underlying hardware while providing high level programming features.

### Compiling

On macbook you can do this to compile your code: 
```bash
cc test.c
```

And if you wanna update the output file name you can do that:
```bash
cc -o name test.c
```

C defines two possible execution environments: freestanding and hosted. Freestanding environment may not provide an operating system and is typically used in embedded programming. It don't access the I/O operations. Hosted environment is generally used code interface. 