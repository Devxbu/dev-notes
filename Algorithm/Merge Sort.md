M Way Merge sort is basically the merging of 2 ordered lists into 1 ordered list. It works in an iterative way. We can give an example like this 

```c
int j, k, i = 0, 0, 0;
int a[4] = {2, 8, 15, 18};
int b[4] = {5, 9, 12, 17};
int c[8];
```

We have 2 sorted lists and we want to put them in a sorted form inside list c.

We will go through list a with variable i, list b with variable j and list c with variable k. 

1. We compare whether the 0th element of a is larger or smaller than the 0th element of b. The 0th element of a is smaller, so we give the 0th element of a to the 0th element of c and increment variables i and k by one.
2. Since we have increased variable i by 1, we start the comparison at element 0 of b and element 1 of a. Whoever is smaller, the 0th element of b is smaller. Now we write the 0th element of b into the 1st element of c and increment j and k by one.
3. we will do this until we run out of lists a and b.

The space complexity and time complexity of merge sort will be O(m + n) (m is the length of list a, n is the length of list b) 

Below is an example for m way merge sort

```c
int* mergeSort(int a[], int b[], int m, int n){
	int c[m+n];
	int j, k, i = 0, 0, 0;
	
	while (i <= m && j <= n){
		if (a[i] < b[j]){
			c[k++] = a[i++];
		} else {
			c[k++] = b[j++];
		}
		
		for(; i <= m; i++){
			c[k++] = a[i];
		}
		
		for (; j <= n; j++){
			c[k++] = b[j];
		}
	}
	return c;
}
```

There will be more than one pattern for trying to sort more than 2 lists with merge sort. we can do each list at the same time. we can merge sort the lists with merge sort by sorting both halves of the lists, we can merge sort the first two lists with merge sort and sort the other lists with the newly created list, and vice versa. In this way we can sort more than 2 lists with merge sort using patterns as we wish. The name of this merge sort is “m way merge sort”.

Now we will examine normal merge sort, not m way merge sort. Merge sort works recursively. To use m way merge sort we need to have a minimum of 2 sorted lists, but in merge sort we split the given list into chunks and sort and merge the elements with 2 way merge sort. The complexity of the algorithm is O(n log n). 

1. a = \[9, 3, 7, 5, 6, 4, 8, 2]
2. \[3,9] \[5,7] \[4,6] \[2,8]
3. \[3,5,7,9] \[2,4,6,8]
4. \[2,3,4,5,6,7,8,9]

Now we will look at the divide and conqure approach, which allows us to combine all the elements in a list by sorting them by separating them from each other, which is also recursive and has complexity O(n).

```c
int list[8] = {9, 3, 7, 5, 6, 4, 8, 2}

void mergeSort(l, h){
	if (l < h){
		int m = (l + h) / 2;
		mergeSort(l, mid);
		mergeSort(mid + 1, h);
		merge(l, m, h);
	}
}
```

## Pros and cons of merge sort

### Pros
1. Can be implement on large size lists
2. Suitable for linked list
3. External sorting (Not using the sizes of the lists in the ram it using only 2 elements of space)
4. Stable
### Cons
1. Extra space for sorting
2. Merge sort make the array the smallest it can took long time to other sorting algorithms
3. Recursive
