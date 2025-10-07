
Class: #CO1103 
Date: 07-10-2025
Teacher: #DrPaulaSeveri 
## Functions

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
1 -> dog    <- violates uniqueness
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
3 ->  ___    <- violates totality 
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
	