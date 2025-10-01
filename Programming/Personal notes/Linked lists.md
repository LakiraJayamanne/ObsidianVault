Date: 20-08-2025
Wider topic: #datastructures
Related: [[Arrays]], [[Time Complexity]]

##### Anatomy of a list:

- Say we have a list called "list" and it has 5 nodes in it. This is what the layout would look like. 

```python
list = head -> node -> node -> node -> tail -> None
```

- The first node is always called the head, and the last is always called the tail.

##### Pointers:

- Let's say we have call a pointer called A. We firstly set the pointer A to the head of a list.

```python
A = head
```

- We can move it once or twice or thrice by giving it the command ".next" however many times. For example, if I wanted to move A once;

```python
A = A.next
```

- When the **next** command is declared, the pointer is set to the next node. Hence, the value stored in the pointer will change unless stored elsewhere. If the pointer is currently at the tail node, **.next** will point to "[None]". Because there is nothing else to point to after [None], if A = None, A.next will crash. This is why conditions such as **while node** or **while node and node.next** are used.


![[LC 876.png]]