	
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

## Range (stop)

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


## Range (start, stop[,step])


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


# While loop

- First declare a variable as for counter and set it to 0.
- Once the first statement is printed, the variable "counter" is increased by 1.
- Determine if loop should continue

```python
counter = 0

while counter < 10:
	print("Welcome to Python")
	counter =+ 1
```

### Break

- A break statement causes an exit from the innermost containing while, do, for

```python
for I in range (10):
	if userID[I] == targetID
		index = I
		break
```

### Continue

- The continue statement causes the innermost loop to start the next iteration immediately

```python
for I in range (10):
	if userID != -1:
		continue
	print("UserID " + i + " :" + userID)
```
