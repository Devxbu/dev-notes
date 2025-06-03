
A static array is an array whose size is always constant and can hold only as much data as its size. When we want to pull an element from an array, we write the name of the array and the index of the element we want to pull and the data is pulled in constant time, O(1).

```c
int x[5] = [1,2,3,4,5];

x[0] // 1
x[1] // 2
// ...
x[4] // 5
```

When we want to add any data to the array, all elements will be shifted to one side and will take O(n) time to complete. In the same way, if we want to delete data from the array, all elements are shifted and it takes O(n) time to complete.

Dynamic arrays are arrays whose size can be automatically increased according to the data added to it. Depending on the programming language used, the memory footprint can be increased by 1.5 to 2 times as the array is expanded

### Pros of Arrays
- It takes O(1) time to access the data
- It is easy to delete data from the end of the array or add data to the end of the array
- Each byte is allocated side by side in memory, making it easy to navigate

### Cons of Array
- Excess memory usage
- Deleting and adding data from the array takes too much time O(n)
- Expanding the array is also time consuming O(n)