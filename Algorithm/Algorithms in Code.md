```
def linear_search(list, target):   // A linear search algorithm
	for i in range(0, len(list)):  // Look at the all elements in the list
		if list[i] == target:   
			return i
			
	return "Target is not found."
```

This code will continue as long as the list is long, which makes us call the time complex O(n)

```
def binnary_search(list, target):  // A binnary search algorithm 
	first = 0                      // Firstly define the left identificator 
	last = len(list) - 1           // After that define the right identifactor
	
	while first <= last:         
		mid = (first + last)//2    // Get the middle element on the list
		if list[mid] == target:    // If it's equal to the result return
			return mid
		elif list[mid] < target:   // If it's smaller than the target divide list
			first = mid + 1
		else:                      // If it's bigger than the target divide list
			last = mid - 1
			
	return  "Target is not found"
```

This code halves the length of the list each time, so the time to do this is O(log n).