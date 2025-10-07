Class: #CO1103 
Date: 07-10-2025
Teacher: #DrPaulaSeveri 
# Notes:

- Definition of a function
- Domain, Co-Domain
- Different ways to describe a function
- Image (or range)

### What is a function in maths?

- Function machine: transforms input values into output values. In maths, we abstract from the process. Our goal is a definition that is *general and abstract*

### Functions link things together

```python
#inputs   #function  #output
x1    ->    f    ->    y1
x2    ->    f    ->    y2
x3    ->    f    ->    y3
```

- In maths, a function is a *link* (association/mapping) between inputs and outputs with *two key properties*:
	- Totality: every input has an output
	- Uniqueness: each input has exactly one output


- Example_1: 

	- Input set: A = {1,2,3}
	- Output set: B = {cat,dog}

	- Is this a function? *NO*

``` python
1 -> cat
1 -> dog    <- VIOLATES UNIQUENESS
2 -> cat
3 -> cat
```


- Example_2:

	- Input set: A = {1,2,3}
	- Output set: B = {cat,dog}

	- Is this a function? *NO*

```python
1 ->  cat
2 ->  dog
3 ->  ___    <- VIOLATES TOTALITY
```


- Example_3: 

	- Input set: A = {1,2,3}
	- Output set: B = {cat,dog}

	- Is this a function? *YES*

```python
1 -> cat
2 -> cat          # DOES NOT VIOLATE ANYTHING
3 -> dog
```

## Domain and Co-Domain

Inputs and outputs in mathematics. 

- Instead of "sets of inputs", we say **domain**
- Instead of "sets of outputs", we say **codomain**

```python
f : A -> B     # FORMAL WAY TO SPECIFY DOMAIN AND CODOMAIN

# A is the domain of f (sets of inputs)
# B is the codomain of f (sets of outputs)
```

- The function, is a link between the elements of A and B that satisfied:
	- *Totality*: Every element **a ∈ A** is linked to some element **b ∈ B**
	- *Uniqueness*: This element **b** is unique; that is, if **a** is linked to both **b** and **b'**, then **b = b'**


## Methods of describing functions

1. Using a table
2. Arrow Diagram
3. Algebraic Definition
4. Define by cases
5. Define as a set of pairs

### 1. Tables for functions

``` python
double : {0,1,2,3,4,5,6,7}  ->  Z

# the domain is {0,1,2,3,4,5,6,7}
# the co-domain is Z (integers)
```

| x      | 0   | 1   | 2   | 3   | 4   | 5   | 6   | 7   |
| ------ | --- | --- | --- | --- | --- | --- | --- | --- |
| double | 0   | 1   | 4   | 6   | 8   | 10  | 12  | 14  |

The first row represents the input values. The second row contains the outputs.


### 2. Arrow Diagrams

```python
f : {cat,dog,robin} -> {2,4}
```

![[Functions - Arrow diagrams.png]]

Each element in *A* is mapped to a **unique** element in *B*

### 3. Algebraic function representation

```python
double : {0,1,2,3,4,5,6,7} -> Z

double(x) = 2 · x     # algebraic expression
```

- Square : R -> R
	- square(x) = x^2 for any x ∈ R

- double: Z -> Z
	- double(x) = 2 · x for any x ∈ Z

- average: R × R -> R
	- average(x,y) = (x+2)/2 for any x,y ∈ R


### 4. Defining a function by cases

Pixels = {n ∈ N: 0 <= n <= 255}

quantise : Pixels -> Pixels

quantise(n):
	26   if  0<=n<=51
	78   if  52<=n<=103
	130  if  104=n<=155
	182  if  156<=n<=207
	234  if  208<=n<=255

### 5. Defining a function as a set

Input-output connection = a pair

*double* as a set of pairs:

*double* = { (0,0), (0,1), (2,4), (3,6), (4,8), (5,10), (6,12). (7,14) }

First element in a bracket is the input, second element is the output.

## Partial functions

Let *A* and *B* be sets and *S ⊂ A*. A *partial function f, from A to B* is a function from *S* to *B*. 

When *f* from *A to B* is a function, we say that the function is **total** to stress the totality. 

