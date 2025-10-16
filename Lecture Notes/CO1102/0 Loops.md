
Class: #CO1102
Date: 16-10-2025
Teacher: #MohammaedZare #EmmanuelTad

# For Loops

```python
for each number in a sequence of numbers
	Do something

for each item in some List
	Do something

for each character in some string
	Do something

for each line in some files
	Do something
```

# Range (stop)

- Iterates over integers from 0 to stop-1. That is, integers in [0,stop]
- Begins at 0
- Stops (exits the loop) when it gets to stop

### Example:

- Simple loop

```python
for value in range (10):
	print(value)

#output: 
0
1
2
3
4
5
6
7
8
9 
```


# Range (start, stop[,step])


- Starts with the integer start
- Stops (exits the loop) when it gets to stop
- Default step size is 1 (but can have other step sizes)

### Example:

- Simple loop

```python
for value in range(12, 0, -2):
	print(value)	

#ouput
12
10
8
6
4
2
```

