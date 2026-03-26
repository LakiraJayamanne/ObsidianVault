Class: #CO1103
Date: 18-03-2026
Related: #ProofByInduction #Proof #NaturalNumbers

## Topic Overview

- Proof by induction is used to prove statements about [[natural numbers]]
- Two steps: the **base case** and the **inductive step**
- Works like dominoes — prove the first falls, prove each one knocks the next, therefore all fall

## Notes

### Base Case

- Prove that P(0) or P(1) is true (whichever is the starting value)
- This establishes the foundation the rest of the proof depends on

### Inductive Step

- Assume P(k) is true — this is called the **inductive hypothesis**
- Using that assumption, prove that P(k+1) must also be true
- This shows the "domino effect" holds for every step

### Why It Works

- The base case proves the first domino falls
- The inductive step proves every domino knocks the next one over
- Together, they guarantee every P(n) is true for all natural numbers from the base case onward

## Key Definitions

| Term | Definition |
|------|------------|
| Proof by Induction | A proof technique for statements about natural numbers using a base case and inductive step |
| Base Case | Proving the statement holds for the initial value (usually n=0 or n=1) |
| Inductive Hypothesis | The assumption that P(k) is true, used to prove P(k+1) |
| Inductive Step | The part of the proof that derives P(k+1) from the assumption P(k) |

## Examples

### Sum of First n Natural Numbers: 1 + 2 + ... + n = n(n+1)/2

**Claim:** For all n ≥ 1, 1 + 2 + ... + n = n(n+1)/2

**Base case (n=1):**

```
LHS = 1
RHS = 1(2)/2 = 1
LHS = RHS ✓
```

**Inductive hypothesis:** Assume 1 + 2 + ... + k = k(k+1)/2

**Inductive step:** Prove 1 + 2 + ... + k + (k+1) = (k+1)(k+2)/2

```
LHS = [1 + 2 + ... + k] + (k+1)
    = k(k+1)/2 + (k+1)          [by inductive hypothesis]
    = (k+1)[k/2 + 1]
    = (k+1)(k+2)/2
    = RHS  ✓
```

QED.

## Common Mistakes

- Forgetting the base case entirely
- Circular reasoning in the inductive step (using what you're trying to prove)
- Assuming P(k+1) is true instead of actually proving it follows from P(k)

## Questions / Gaps

- Are there cases where induction applies to integers beyond natural numbers (e.g. strong induction)?
