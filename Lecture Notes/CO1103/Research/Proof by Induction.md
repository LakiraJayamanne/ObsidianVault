Class: #CO1103
Date: 18-03-2026
Related: #ProofByInduction #Induction #NaturalNumbers
Sources: [[YouTube]]

## Topic Overview

[[Proof by Induction]] is a technique for proving a statement is true for all positive integers. It works like falling dominoes — prove the first falls (base case), prove each knocks the next (inductive step), and all must fall.

## Key Concepts

- **Base Case** — prove the statement holds for the starting value (usually n=1)
- **Inductive Hypothesis** — assume the statement is true for some arbitrary k
- **Inductive Step** — using that assumption, prove it holds for k+1

## Notes

### The Two-Step Process

1. **Base Case** — prove the statement is true for the smallest value (typically n=1)
2. **Inductive Step**
	- State the inductive hypothesis: assume true for n=k
	- Prove it follows for n=k+1

### Why It Works

Think of dominoes — if you can prove the first one falls, and that any falling domino knocks the next one over, then every domino in an infinite sequence will fall.

## Key Definitions

| Term | Definition |
|------|------------|
| Mathematical Induction | A proof technique for statements about all positive integers |
| Base Case | Proving the statement holds for the initial value (n=1 or whatever the threshold is) |
| Inductive Hypothesis | The assumption that the statement is true for n=k |
| Inductive Step | Proving the statement is true for n=k+1 using the inductive hypothesis |

## Examples

### Sum of Positive Integers: 1 + 2 + ... + n = n(n+1)/2

**Base case (n=1):**
```
LHS = 1
RHS = 1(1+1)/2 = 1
LHS = RHS ✓
```

**Inductive hypothesis:** assume 1 + 2 + ... + k = k(k+1)/2

**Inductive step:** prove for n = k+1
```
(1 + 2 + ... + k) + (k+1)
= k(k+1)/2 + (k+1)          [by inductive hypothesis]
= (k(k+1) + 2(k+1)) / 2
= (k+1)(k+2) / 2             [matches formula for n=k+1] ✓
```

QED.

## Common Mistakes

- **Pattern testing isn't proof** — checking n=1,2,3 shows a pattern but doesn't guarantee it holds forever (could fail at n=15 or n=100)
- **Skipping the base case** — without it the chain has no starting point
- **Wrong substitution** — forgetting to use the inductive hypothesis to simplify the left side
- **Assuming n=1 is always the base** — some statements only hold above a certain threshold (e.g. n>5)

## Sources

- [Mathematical Induction Practice Problems](https://www.youtube.com/watch?v=tHNVX3e9zd0) — The Organic Chemistry Tutor
- [Proof by induction](https://www.youtube.com/watch?v=wblW_M_HVQ8) — Khan Academy
- [Proof by Mathematical Induction](https://www.youtube.com/watch?v=dMn5w4_ztSw) — Learn Math Tutorials

## Questions / Gaps

- Can induction be used for integers beyond natural numbers? (see [[Strong Induction]])
