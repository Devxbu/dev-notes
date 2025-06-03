## What is a algorithm

Algorithms are the name of all the steps followed when finding a solution to a problem. Today, algorithms try to solve a problem in the most efficient way. When faced with a problem, the algorithms to be chosen are not always the same, this depends on the work to be done and the problem, it is important to use the right algorithm in the right place.

## Efficiency

#### Time Complexity

Algorithms spend a certain amount of time and space in memory while they are	running, we call them complexity, as mentioned, complexity is divided into 2, time complexity and space complexity, time complexity is the calculation of the time required for the completion of an algorithm for the worst case scenario, for example, if it is requested to find the number 3 among the numbers from 1 to 100 in a linear search algorithm, it will be found in these 3 stages, but if it is requested to find the number 100, then it will be found in the 100th stage. In this way, the time equivalent of this list is the size of the list, we give it the letter n.

#### Space Complexity

Space complexity works similarly, let's go through the linear search algorithm again. Our first case is to find 3 out of the numbers between 1 and 100, in the first step it took up x amount of memory, in the second the space it spent in memory became 2x, when the result was found it became 3x. Here again the space complexity is determined by the worst probability, here again the worst probability is to take up a total of 100x space in memory. Again, in the same way we call the length of the list, that is, the space complexity n

#### Some Big O Notaion Names

`Linear`: it means as long as the given list length. It is shown as O(n)

`Logarithmic`: It is the time equivalent that increases logarithmically depending on the length of the given list. It is expressed as O(log n)

`Constant`: Algorithms that take only one operation to complete are called O(1) algorithms.

`Quadractic`: It increases by two exponents each time. It is shown as O (n^2)

`Quasilinear`: The representation of multiplying by n in a logarithmic manner is O(n log n)

If we were to sort from largest to smallest: Quadractic > Quasilinear > Linear > Logarithmic > Constant

### How To Determine an Algorithm Complexity

When trying to find the complexity of an algorithm, we need to look at how many times it goes over the data. If there is a loop anywhere, the complexity	is n. If there is another loop inside any loop, the complexity is n^2. If half of the list starts to go in each step, it is log n.