Class: #CO1103 
Date: 10-10-2025
Teacher: #DrPaulaSeveri 
Related: #Functions 
Week: #W2 

# Composition of functions (definition)

$$
\Large g: A -> B
$$

$$
\Large f : B->C
$$


The codomain of g should be the same as the domain of f

- The composition of f and g, denoted by f $\circ$ g : A -> C where :

$$
\Large f \circ g(x) = f(g(x))
$$

Example: 

$\Large f(x) = x^2$      $\Large g(x) = x+1$

$\Large f \circ g(x) = f(g(x)) = f(x+1) = (x+1)^2$

## Using arrow diagrams

![[composition arrow diagram.png]]


# Connections with computer science

Applications of function composition:

- Pipelines & workflows: Output of one function becomes input of the next
- Data Processing: Chaining transformations (e.g., filter -> map -> reduce)
- Graphics: Apply multiple transformations in sequence (scale -> rotate -> translate)
- Cryptography: Layered encryption schemes (multiple ciphers applied in order)
- Software Design: Modular code by composing small functions