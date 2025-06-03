
Linked lists consist of nodes (containing data and a pointer to the next node) connected to each other. Linked lists do not use side by side space in ram like arrays. Linked lists are shuffled in ram and are connected to each other by a pointer inside the node pointing to the next node. We have a head, which always points to the first element of the linked list, and to navigate through the list we start at the head and use the pointers of the nodes to navigate between the nodes. In Array it takes O(1) (constant time) to access an element, in Linked lists it takes O(n) (Linear time) to access an element. There is an example for the node and linked list

```python 
class Node: 
	def __init__(self, data):
		self.data = data
		self.next_node = None

class LinkedList:
	def __init__(self):
		self.head = None
```

### Navigate within a Linked List

To navigate inside a linked list we use the next of the nodes. Linked lists are connected to each other through the next variable and we do this by using pointers in C language by pointing to each other. Let's examine it with an example

```python
def printList(self):
	current = self.head
	
	while current.next_node:
		print(current.data)
		current = current.next_node
```

In the example, we first define our self.head to a variable called current, start a loop that will continue until the other nodes pointed to by this variable are None, then print the data of each node and replace the current with the node it points to.

### Adding New Node To Linked List

I will show 2 examples to add a new node to the linked list, one at the end and one at the index we want.

```python
def addToEnd(self, data):
	newNode = Node(data)
		
	if self.head is None:
		self.head = newNode
		return
		
	current = self.head
	while current.next_node:
		current = current.next_node
		
	current.next_node = newNode
```

This example is a code to add an element to the end of the list. At first we sent the data sent to the function into the node class we created and it gave us a node, then we checked if there were any elements in the linked list, if there were not, it would add them directly. After this check, we go to the end of the linked list and update the next_node of the last element with the node we just created.

```python
def addWithIndex(self, data, index):
	newNode = Node(data)
	i = 0
	
	current = self.head
	while i < index:
		if current.next_node:
			current = current.next_node
		else:
			return "Your index is so big for list"
	
	newNode.next_node = current.next_node
	current.next_node = newNode
```

This example adds an element to the given index of the list. Unlike the other code, we do not go through the entire list until we reach the index, and after reaching the index, we give the node that current shows to the next node of newNode, and then we replace current's next with newNode.

### Deleting Node in Linked List

In order to delete an element from our list, we will link the node pointed to by the previous node we are deleting to the node pointed to by the node we are deleting and in this way nothing will hold the node we are deleting and we will not be able to access it from our linked list. Let's examine it with the following example

```python
def delete(self, key):
	curr = self.head
	prev = None
	isFound = False
	index = 0

	while !isFound: # Node bulunana kadar tekrar edecek
		if curr.data == key:
			if prev == None: # Eger node ilk data ise self.head oynatilir
				self.head = self.head.next 
			else: # Degilse bir onceki node bir sonraki node ile baglanir
				prev.next = curr.next
		isFound = True

		if curr.next: # Tail'e gelinmemisse devam eder
			prev = curr # Degiskenler ilerletilir
			curr = curr.next
		else: # Key bilgisi listenin icerisinde yoksa calistirilir
			return "Node isn't in the list"
```

## Doubly linked list

In doubly linked lists, each node points to both the next node and the previous node. The head, i.e. the pre of the node at the beginning, and the tail, i.e. the next of the node at the end, show a null value. Below is how the node looks in code.

```python
class Node
	def __init__(self, data):
		self.prev = None
		self.data = data
		self.next = None
		
class DoublyLinkedList:
	def __init__(self):
		self.head = None
```

When we want to add a new node to this doubly linked list (I will give 3 examples, last, first and last) we will need to add it through the nexus of the previous node and the prefix of the added node will point to the previous node.

```python 
"""Adds a new node to the end of the list"""
def append(self, data):
	new_node = Node(data) 
	# If the list is empty, the new node becomes head 
	if not self.head: 
		self.head = new_node 
	# If the list is not empty, let's reach the last node and add the new node 
	else:
		last = self.head 
		while last.next: 
			last = last.next 
	# Let's connect the last node to the new node 
	last.next = new_node 
	new_node.prev = last 
	
"""Adds a new node to the beginning of the list"""
def prepend(self, data): 
	new_node = Node(data) 
	# The next of the new node becomes the current head 
	new_node.next = self.head 
	# If head exists, its prev becomes the new node 
	if self.head: 
		self.head.prev = new_node 
	# The new node is now the head 
	self.head = new_node 
	
"""Adds a new node after the specified node"""
def insert_after(self, prev_node, data):  
	# Let's check the existence of the previous node 
	if not prev_node: 
		print(“Previous node not found”) 
	 # Let's create a new node 
	 new_node = Node(data) 
	 # The next of the new node becomes the next of the previous node 
	 new_node.next = prev_node.next 
	 # The next of the previous node is now the new node
	 prev_node.next = new_node 
	 # The prev of the new node becomes the previous node 
	 new_node.prev = prev_node 
	 # If the new node has a next, its prev becomes the new node 
	 if new_node.next: 
		 new_node.next.prev = new_node
```

Removing nodes from the list will also be much easier than normal link lists.

```python
def delete_node(self, key):
        """Deletes the node with the given value"""
        # Create a temporary node and synchronize it to head
        temp = self.head
        
        # If the node to be deleted is head
        if temp and temp.data == key:
            self.head = temp.next
            if self.head:
                self.head.prev = None
            temp = None
            return
        
        # Find the node to delete
        while temp and temp.data != key:
            temp = temp.next
            
        # If key is not in the list
        if not temp:
            print(f"{key} değeri listede bulunamadı")
            return
            
        # connect the previous node of temp to the next node of temp
        if temp.prev:
            temp.prev.next = temp.next
        
        # connect the next node of temp to the previous node of temp
        if temp.next:
            temp.next.prev = temp.prev
            
        # let's free temp
        temp = None

```
```