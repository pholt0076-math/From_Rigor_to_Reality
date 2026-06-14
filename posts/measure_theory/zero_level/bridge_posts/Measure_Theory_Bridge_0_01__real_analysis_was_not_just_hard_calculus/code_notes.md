# Measure Theory Bridge 0.01
## Pointwise Convergence Is Not Uniform Convergence

Status: drafted
Role: Python companion document for Content Post 1 of 42
LinkedIn companion to: **Real Analysis Was Not Just Hard Calculus**

## Code purpose

This code note illustrates one of the central lessons of Real Analysis:

pointwise convergence is not the same as uniform convergence.

That distinction matters because it shows why infinite processes require careful control.

The example is:

fₙ(x) = xⁿ on [0, 1]

For every x with 0 ≤ x < 1, xⁿ → 0.

But at x = 1, xⁿ = 1 for every n.

So the pointwise limit is:

f(x) = 0 for 0 ≤ x < 1  
f(1) = 1

The limit function is discontinuous, even though each fₙ is continuous.

That is one reason Real Analysis becomes the doorway to Measure Theory:

we begin asking where the bad behavior occurs.

## Python demo

```python
import numpy as np

def f(n, x):
    return x ** n

xs = np.linspace(0, 1, 11)

for n in [1, 2, 5, 10, 25, 50]:
    values = [round(f(n, x), 4) for x in xs]
    print(f"n = {n:>2}: {values}")

print()
print("At x = 0.5, x^n tends to 0.")
print("At x = 0.9, x^n also tends to 0, but more slowly.")
print("At x = 1.0, x^n stays equal to 1 forever.")
```

## Interpretation

The sequence fₙ(x) = xⁿ behaves differently depending on where x is located.

For every point less than 1, the sequence tends to 0.

At the single point x = 1, the sequence stays fixed at 1.

So the limiting behavior is controlled by a set:

{x = 1}

This is the conceptual bridge.

Real Analysis notices the failure.

Measure Theory will eventually ask:

How large is the set where the failure occurs?
