## Arrays

	Arrays are data structures that can hold and access one or more data. Arrays 
	are divided into two: homogeneous and heterogeneous.
	Homogeneous arrays require the data types in the array to be the same. 
	Heterogeneous arrays can also contain different data types.
	
	Below is an example of a homogeneous array

```
#include <stdio.h>

int main(){
	int homogeneousList[10] = [1, 2, 3, 4, 5];
}

```

	Below is an example of a heterogeneous array 

```
heterogeneous_list = [1, "a", 2, "b"]
```

	Indexes are used to read arrays, these indexes show the data in the list in 
	an orderly manner (like pointers). Indexes start from 0 and continue until 
	the length of the list - 1. An example is shown below.

```
my_list = [1, 2, 3, 4]

result_1 = my_list[0] // Equal to 1
result_2 = my_list[2] // Equal to 3
result_3 = my_list[3] // Equal to 4
```

	To search for data in arrays, we follow a linear method (if the list is 
	sorted, we can make it more efficient by using the binary search method). We 
	traverse the list and compare elements until we find the same element. An 
	example is given below

```
#include <stdio.h>

int main() {
	int myList[5] = [0, 1, 2, 3, 4];

	for (int i = 0; i < 5; i++){
		if (myList[i] == 2){
			printf("2 was founded at %d index", &i);
			
			break;
		}
	}
}
```

	If adding data to arrays is static, it is not possible to add new data 
	because the array has a reserved place in memory and since it is a static 
	array, the designated place cannot be increased by adding new data, so it 
	crashes. However, data can also be added to empty places in static arrays, 
	there is an example below.

```
#include <stdio.h>

int main() {
	int myList[5] = [0, 1, 2, 3];
	myList[5] = 4;
	
	printf("%d", &myList[5]);	
}
```

	To delete an element from an array, you need to move that element by 
	shifting it, there is an example below.

```
#include <stdio.h>

int main(){
	int index = 2;
	for (int i = index; i < 4; i++) {
	    numbers[i] = numbers[i + 1];
	}
	numbers[4] = 0; 
}
```

## Linked List

	Why we using the linked list? Arrays are perfect data structures for 
	storage. It's search and accessing operations time complexity is O(1) 
	(Constant Time). But inserting and deleting operations goes linear that 
	makes O(n) time complexity. That reason to why we using linked list.

	How that works? Linked list has take 2 values: Data, and next value adress. 
	The first value is called head and the last value is called tail. The 
	address of head is not linked by any value and tail does not link any 
	address of any value. As an example, we can consider the following diagram 
	(x, y, z and a are defined as values, and the numbers are addresses)
	
	[x, 1003] - [y, 1004] - [z, 1005] - [a, 1005]
	   *Head*      *1003*      *1004*      *Tail*

```python
class Node: 
	def __init__(self, data):
		self.data = data
		self.nex_node = None
	
	def __repr__(self):
		return "<Node Data: %s>" %self.data
	
N1 = Node(10)         // N1 -> 10
N2 = Node(20)         // N2 -> 20
N1.next_node = N2     // N1.next_node -> 20
	
Class LinkedList:
	def __init__(self):
		self.head = None
	
	def add(self, data):
		newNode = Node(data)
		
		if self.head is None:
			self.head = newNode
			return
		
		current = self.head
		while current.next_node:
			current = current.next_node
		
		current.next_node = newNode
		
	def key(self, key):
		current = self.head
		while current:
			if current.data == key:
				return current
			else:
				current = current.next_node
		return None
			
	def list(self):
		temp = self.head
		while temp:
			print(temp.data, end="->")
			temp = temp.next_node
			
	 def insert(self, data, index):
        new_node = Node(data)
        
        # Başta ekleme durumu
        if index == 0:
            new_node.next = self.head
            self.head = new_node
            return
            
        # Araya veya sona ekleme durumu
        current_node = self.head
        for _ in range(index - 1):
            if not current_node:  # Eğer index diziyi aşarsa
                print("Index out of range!")
                return
            current_node = current_node.next
            
        # Yeni node'u araya yerleştir
        new_node.next = current_node.next
        current_node.next = new_node


```


	As in the example, we proceed from the next nodes to the end to traverse the 
	list.

	The operations of extracting data from the desired location and adding data, 
	which play the most role in the use of linked lists, have O(1) complexity in 
	line with the method they work. Because instead of shifting the entire list, 
	the pointers of the nodes change.
![[Deleting In Link List.png]]


## Sorting Algorithms

### Merge Sort

	