Stack is a LIFO data structure (Last-In First-Out). stores objects into a sort of vertical tower. push() method add to the top, pop() method remove from the top. 

Imagine you have a 5 video game cd, and you wanna put that cds in the table in vertical order. You put first minecraft cd, after doom cd, gta cd, guitar hero cd and finally you put the overwatch cd. What do you make for the get minecraft cd? You have to get cd on the top firstly. pop() the cds while when you reach to the minecraft cd.

We have 5 functions for the Stack data type: 
- push() adds a new element to the end of the list
- pop() removes the last element of the list
- peek() returns the last element in the list
- isEmpty() checks if the list is empty
- search() searches for the given element in the list

Let's see stacks in code

```c
#include <stdio.h>
#include <stdlib.h>

int *arr;
int size = 2;
int curr = 0;

int pop(){
	if (curr <= size/4){
		int *new_arr = (int*)malloc(sizeof(int)*size/2);
		for (int i = 0; i < size/2; i++){
			new_arr[i] = arr[i];
		}
		free(arr);
		arr = new_arr;
		size /= 2;
	}
	return arr[--curr];
}

void push(int a){
	if(curr >= size){
		int *new_arr = (int*)malloc(sizeof(int)*2*size);
		for (int i = 0; i < size; i++){
			new_arr[i] = arr[i];
		}
		free(arr);
		arr = new_arr;
		size *= 2;
	}
	arr[curr++] = a;
}

int main(){
	arr = (int*)malloc(sizeof(int)*2);
	push(10);
	push(20);
	push(30);
	printf("pop: %d\n", pop());
	printf("pop: %d\n", pop());
	return 0;
}
```

Queue is a FIFO data structure (First-In First-Out). stores objects like a line of people.

Imagine a grocery store with a line at the checkout, the first person in this line, the person at the top of the line, is the first person to be dealt with, and when he is done, the line moves to the next customer, and so on until the line is over.

We have 6 functions for the Queue data type:
- offer() adds an element to the end of the list
- poll() deletes the element at the beginning of the list
- peek() looks for the element at the top of the list
- isEmpty() checks if the list is empty
- size() returns the size of the list
- contains() checks if the list contains the specified element