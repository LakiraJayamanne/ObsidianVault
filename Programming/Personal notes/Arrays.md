Date: 20-08-2025 
Wider topic: #datastructures 
Related: [[Linked lists]], [[Time Complexity]]

### Anatomy of an array: 

- An array is an ordered collection of elements stored in a sequence
- In python, arrays are usually represented as lists
- Each element has an index (starting with 0)
- The first element is array[0] and the last element is array[-1]

Example: 

```python
arr   =   [10, 20, 30, 40, 50]
# Indexes   0   1   2   3   4
```


### Indexing and iteration:

We can access elements by index or loop through the whole array:

```python
arr = [1, 2, 3, 4]

print(arr[0])    #1
print(arr[-1])   #4

for num in arr:  #iteration
	print(num)

```


### Useful functions with arrays:

- Finding length of an array

```python
len(arr)
```

- Finding the sum of elements in an array

```python
total = sum(arr)
```

- Finding largest and smallest elements in an array

```python
largest = max(arr)

smalles = min(arr)
```


### Slicing:

- Python supports slicing arrays to get sub-lists

```python
arr = [1, 2, 3, 4, 5]

print(arr[1:4]) #prints everything from index 1 up to, but not including, index 4
print(arr[:3]) #prints everything up to index 3
print(arr[2:]) #prints everything from index 2
print(arr[::-1]) #print everything in reversed order (5, 4, 3, 2, 1)
```


### 2D Arrays (Matrices):

- A list of lists in python can be represented as a 2D array

```python
grid = [
	[1, 2, 3],   #   0,0  0,1  0,2
	[4, 5, 6]    #   1,0  1,1  1,2
]

print(grid[0][1])  # 2

print(grid[1][2])  # 6
```

- First index = row
- Second index = coloumn



### Common patterns in array problems

#### Prefix Sums:

- Efficient ways to get sum of sub-arrays:

```python
arr = [1, 2, 3, 4]

prefix = [0] * (len(arr) + 1)

for i in range(len(arr)):
	prefix [i+1] = prefix[i] + arr[i]
	
#sum of arr[1:r] = prefix[r] - prefix [1]
```

#### Sliding window: 

- For subarray problems (e.g. "max sum of k-length subarray"):

```python
arr = [1, 2, 3, 4, 5]
k=3

window_sum = sum(arr[:k])
max_sum = window_sum

for i in range(k, len(arr)):
	window_sum += arr[i] - arr[i-k]
	max_sum = max(max_sum, window_sum)
	
```

#### Two pointers:

- Used on sorted arrays for pair problems:

```python
arr = [1, 2, 4, 7, 11, 15]
target = 15
1, r = 0, len(arr) - 1

while 1 < r:
	s = arr[1] + arr[r]
	if s == target:
		print(arr[1], arr[r]) # found pair
		break
	elif s < target: 
		1 += 1
	else:
		r -= 1
		
```