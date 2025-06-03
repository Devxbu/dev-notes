
To understand pointers better, let's first examine how variables work. First, after we write our variable, we allocate bytes in memory according to the type of variable (int -> 4 bytes, float -> 4 bytes, char -> 1 byte). When we perform an operation on our variable, our compiler finds our variable in ram and performs the operation. As we will see in more detail shortly, the ampersand “&” gives us the location of our variable stored in memory.

Pointers are simply a type of variable that holds the address of a variable in memory. When we define a pointer, we specify the data type of the variable we want it to point to in memory. Therefore, our pointer takes up as much memory space as the value it points to.

```c
int a = 4; // This is a normal varaible declaration.
int * p = &a; // This is a pointer varaible declaration. (& is get the address of a varaible)

// p -> address *p -> value at address
```

If we try to print the variable p or a& to the screen, it will print the address of variable a in memory. If we try to output p& to the screen, it will show where p is stored in memory. If we print p* to the screen, it will give the defined value of a.

```c
*p = 8;
```

Changing the value of p in this way allows us to change the value of a, which is called derefferancing.

```c
p + 1;
*(p + 1);
```

This code adds 4 to the address held by our pointer. The reason why it adds 4 even though we did + 1 above is that the round of our pointer will make an increment in the form of the amount written *. Since the integer is 4 bytes, it adds 4. Underneath, when we print the value using the * operator, the pointer should express the next integer from a to which the pointer points. This leads us to the array logic. Because arrays are sequential in memory and have the same type, our pointer arithmetic works exactly as it should.

In response to the question why there is no general type for pointers if all pointers hold the address of variables in RAM: pointers organize and access data by type. For example, we have an int variable that starts at 1000 and goes up to 1004 in RAM (int's take up 4 bytes in memory), the address value given to our pointer will be 1000. If the pointers were to have a general type, it would not understand that when the pointer is given the value 1000, it has to take from 1000 to 1004 and process it accordingly.

When we define pointers as we have learned, we write the data type whose address we want to get. So what do we do when we want to write pointers to pointers? We can define pointers by using the * sign one more time for each pointer sign, as in the example

```c
int x = 4;
int *p = &x; // location of x in memory
int **pp = &p; // location of p in memory
int ***ppp = &pp; //location of pp in memory
```

In this way we can write pointers to pointers. When we print this, the variable p holds the value of x and when we write it with * we get the output 4, pp gives us the address of p in memory and ppp gives us the address of pp in the same way even if we use *.

Now that we understand how to use pointers, let's see where we can use them.

First let's look at pointers in function arguments (call by reference)

```c
void inc(int a){
	a++;
}

int main(){
	int a = 4;
	inc(a);
	printf("a = %d", a)
}
```

What do we expect to happen in our code? A variable a is defined and sent to a function that increments a by 1. While we expect the printed value to be 5, 4 is printed. But we have incremented a by one thanks to the function. If we look at the actual working logic, let's say that a temporary variable holding the value of a is sent to the inc function when sending the variable a to the function. This temporary value is updated and when the function is done, this variable is also done and disappears. Let's see what would happen if we did this using pointers

```c
void inc(int* p){
	*p++;
}

int main(){
	int a = 4;
	inc(&a);
	printf("a = %d", a)
}
```

When we do it this way, our output will be 5. We understand the reason why a code like this gives 4 as output, but why will this code give 5 as output? Because we just passed a pointer, a temporary variable was passed to the function, now we passed a different address than the address of the pointer in memory, yes, but the value in it was the value of a stored in memory and the value of the pointer sent did not change. In this way we were able to increment a

C de bir array tanimlamak icin assagidaki kodu kullaniriz ve bu bizim ramimizde ardisik olarak yer kaplayan byteler olur. Bir arrayin ramde kac byte yer kaplayacagini arrayin veri turunun ramde kaplayacagi yer \* kac element oldugu seklinde hesaplariz. 

```c
int main(){
	int a[5]; 
// That's defines an array. And int has 4 bytes, we use 5 int that means that array's space is 20 byte.
}
```

In the Pointer arithmetic, after doing an addition operation with a pointer, we see that the number in the addition operation /* indicates the address as far forward as the number of bytes of the round that the pointer represents. For example, if our pointer p is the pointer of our integer i and i's place in ram is 300, p + 1 will give us an output of 304. It doesn't make much sense to use this with normal data types because we don't know what is stored in ram after the variable and whether it is the same data type. But since arrays are both pipelined and have the same data type, we can use this pointer arithmetic. Let's look at the following example.

```c
int main(){
	int a[5] = {1, 2, 3, 4, 5};
	int *p = &a;
	printf("%d %d", p *p); // For example that prints 300 and 1
	p = p + 1;
	printf("%d %d", p *p); // And that prints 304 and 2
}
```

We will better understand the connection between pointers and arrays with the following example.

```c
int sumOfAllElements(int A[], int size){
	int sum = 0;
	for (int i = 0; i < size; i++){
		sum += A[i];
	}
	return sum;
}

int main(){
	int A[5] = {1, 2, 3, 4, 5};
	int size = sizeof(A) / sizeof(A[0]); // sizeof returns the byte numbers of given element.
	int total = sumOfAllElements(A, size); 
	printf("%d", total); // That prints 15
}
```

VI have written a little code that collects the elements in the given array, this code works fine and the output is correct. What if I didn't give the number of elements in the array and we did the same operation with sizeof in the soae function? Let's examine

```c
int sumOfAllElements(int A[]){
	int sum = 0;
	int size = sizeof(A) / sizeof(A[0]);
	for (int i = 0; i < size; i++){
		sum += A[i];
	}
	return sum;
}

int main(){
	int A[5] = {1, 2, 3, 4, 5};
	int total = sumOfAllElements(A); 
	printf("%d", total); // That prints 1
}
```

The reason why the result is not as expected in this code is that instead of sending the entire array to the function, we actually send a pointer representing the first element of the array. With the indexing method, we have also done some kind of pointer arithmetic to traverse the list, so the first code gave a result as we expected, the second code gave a different result than we expected. 

Now let's look at strings. To define strings, let's first look at how we need to store them. For example, we want to store a word with 5 characters, for this we cannot say the size of the array is 5, we can say a minimum of 6. The reason for this is that in c, when the strings end, the expression “\0” is put at the end, this expression indicates that the string is over. 

```c
int main(){
	char b[5];
	b[0] = 'B';
	b[1] = 'a';
	b[2] = 'h';
	b[3] = 'r';
	b[4] = 'i';
	printf("%s", b); // That cant be return "Bahri" thats generates an error.

	char b[6];
	b[0] = 'B';
	b[1] = 'a';
	b[2] = 'h';
	b[3] = 'r';
	b[4] = 'i';
	b[5] = '/0';
	printf("%s", b); // Now that return "Bahri" with no errors.

	char v[6] = "Verda"; // We can define that way too.
}
```

The fact that arrays and pointers work so similarly does not make them the same type. They are different types, but they can be used in similar ways. In the same way, char arrays can be navigated by using pointer arithmetic. When doing operations on char arrays, we can use '/0' instead of the size of the array. This way we can traverse the array without using the array size.

```c
int main(){
	char x[6] = "Hello";
	char* p = &x;
	
	while (p != '/0'){
		printf("%c", *p);
		p++;
	}
}
```

1 Boyutlu dizlileri inceledik bunlari nasil pointerlar ile kullanabilecegimizi de biliyoruz simdi iki veya daha fazla boyutlu dizileri nasil olustururuz pointirlar ile nasil kullaniriz onlari inceleyecegiz. Bir boyutlu diziler ramde ardisik olarak yer almaktaydi ornegin 200. adreste baslattigimiz 4 elemanli a int dizimiz 212 ye kadar gidecek ve biz buna pointer ile erismek istedigimizde int* p = a diyecektik. Iki boyutlu dizileri ise ramde yan yana yer almis x tane element sayisi ayni dizinin yer almasidir. Assagidaki gibi tanimlanir. 

```c
int B[2][3]; // 2D array. (2 tane art arda dizilmis 3 elementli dizi)
```

Bunu arraylere erismek icin kullandigimiz gibi pointer ile erismeye calisirsak hata alacagiz onun icin yan yana yer alan dizinin eleman sayisi ne ise pointerimiza onu vererek erisecegiz.

```c
int* p = B; // It's False (Starts with 400 sloth in ram)
int (*p)[3]; // That's True

*B = B[0] = &B[0][0]; // 400
*(B + 1) = B[1] = &B[1][0]; // 412
*(B + 1) + 2 = &B[1][2]; // 420
*(*B + 1) = B[0][1] // Value of second value in first array

B[i][j] = *(B[i]+j) = *(*(B + i) + j);
```

