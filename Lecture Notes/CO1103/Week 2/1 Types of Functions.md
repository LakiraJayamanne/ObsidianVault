Class: #CO1103
Date: 09-10-2025
Teacher: Dr Paula Severi
Topic: #Functions
Related: [[2 Composition]], [[3 Inverse]], [[4 Special Functions]]
Builds on: [[0 What is a function]]

# Onto (or surjective) function

A function *f*: A -> B is **onto** (surjective) if *f*(A) = B.

f(A) -> range of f
B -> codomain

Example:

f, f' : A -> B where A = {1,2,3} and B = {Alice, Bob}

![[onto example.png]]


# One-to-one (or injective) function

A function *f*: A -> B is **one-to-one** (injective) if:
	- for any a1, a2 ∈ A, if a1 ≠ a2 then *f*(a1) ≠ *f*(a2).

Example: 

A = {Alive, Bob, Charlie}  B = {A@email.com, B@email.com, C@email.com}

![[onetoone example.png]]


## Bijection

A function *f* : A -> B is **bijective** if *f* is injective (one-to-one) and surjective (onto)

Example:

square : R^{>=0}  ->  R^{>=0}
	square(x) = x^2


# Connection to computer science

- Injective, surjective, and bijective functions link set sizes to combinatorial counting.

- This is important for [Combinatorics], and for analysing the complexity of algorithms


- **Injective (one-to-one)**:
	- Ensures *unique mapping*
	- Example: Hash functions without collisions (ideal case), mapping IDs to users.

- **Surjective (onto)**:
	- Ensures *coverage of all outputs*. 
	- Example: Compiler optimisation mapping expressions to registers - every register is used.

- **Bijective (one-to-one and onto)**:
	- Ensures *perfect reversible mapping*
	- Example: Encoding / Decoding, reversible encryption, or memory address mapping.
