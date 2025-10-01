Date: 20-08-2025
Wider topic: -
Related: [[Arrays]], [[Linked lists]]

### What is Time Complexity?

- Time complexity measures how the runtime of an algorithm grows as input size *n* increases.

- Expressed using *Big-O notation*, which focuses on the dominant term (ignores the constants and smaller terms)

### Common Big-O Complexities:


   *Complexity*        |       *Name*         |             *Example*

   O(1)              |   Constant time    |           Accessing arr[i]
   O(log n )         |    Logarithmic     |            Binary Search
   O(n)              |    Linear time     |  Traversing an array or linked list
   O(n log n)        |    Linearithmic    |       Merge sort, Quick sort
   O(n^2)            |   Quadratic time   |   Nested loops (e.g., bubble sort)
   O(2^n)            |  Exponential time  |      Solving recursive subsets
   O(n!)             |   Factorial time   |     Generating all permutations


### Rules of thumb:

- Drop constants
	- O(2n)  -> O(n)
	- O(n/2) -> O(n)

- Keep the dominant term
	- O(n^2 + n) -> O(n^2)

- Best, Worst, Average cases:
	- Sorting example: Quick sort = O(n log n) average, but O(n^2) worst case.


### Space complexity:

- Measures how much extra memory an algorithm uses.
- Same Big-O rules apply.
- Example:
	- Iterative Fibonacci: O(1) space.
	- Recursive Fibonacci: O(n) space (due to call stack)

### Speed reference diagram

```python
Fastest -------------------------------------------------------------> Slowest

O(1)  ->  O(log n)  ->  O(n)  ->  O(n log n)  ->  O(n^2)  ->  O(2^n)  -> O(n!)
```

