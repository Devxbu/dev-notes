#### What is a Binary Tree

We call a binary tree a data type that consists of nodes that are connected to each other like a tree. In binary trees we have two concepts: parent and children: parents are the nodes that have a node underneath, children are the nodes that have a parent. We can compare this to a family tree: our parents are our parents, but since they also have a mother and father, they are also children. We call the node at the top of our binary tree, which has no parent, root, and the node at the bottom, which has no children, leaf. 

#### Binary treating has a few rules 
1. Each node can have a maximum of 2 children
2. A binary treen can only have one root
3. There can be only one way to reach the node through the tree

Here's an example of manual Binary Tree

```python
class Node:
	def __init__(self, data):
		self.data = data
		self.right = None
		self.left = None

a = Node("a")
b = Node("b")
c = Node("c")
d = Node("d")
e = Node("e")
f = Node("f")

a.left = b
a.right = c
b.left = d
b.right = e
c.right = f

"""
    a
   / \
  b   c
 / \   \
d   e   f
"""

```

## Depth First Values