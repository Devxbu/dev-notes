A function that calls itself from within. Its helps to visualize a complex problem into basic steps, which can be solved more easily iteratively or recursively.

```python
# ITERATIVELY
def walk(steps):
	for step in range(steps):
		print(step)

# RECURSIVELY
def walk(steps):
	if (steps == 0):
		return
	walk(steps - 1)
	print(steps)
```

Recursion is slower but simpler than iteration.