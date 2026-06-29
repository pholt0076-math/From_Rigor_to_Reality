# Code Notes — The Rationals Are Everywhere but Small

## Goal

This companion shows two facts that point in opposite intuitive directions:

1. The rationals are dense: every interval contains rational numbers.
2. The rationals are small in the measure-theoretic sense: a countable list of rationals can be covered by intervals whose total length is as small as we want.

The code does not prove all of measure theory. It makes the mechanism visible.

---

## 1. Generate rational numbers in an interval

A rational number is a number of the form p/q with integers p and q, q ≠ 0.

The function below searches through bounded denominators and returns rational numbers inside an interval.

```python
from fractions import Fraction


def rationals_in_interval(a, b, max_denominator=25):
    """
    Return rational numbers p/q in the open interval (a, b)
    with 1 <= q <= max_denominator.

    This gives a finite computational window into density.
    """
    if not a < b:
        raise ValueError("Expected a < b.")

    found = set()

    for q in range(1, max_denominator + 1):
        # Search enough integer numerators to cover the interval.
        p_min = int(a * q) - 2
        p_max = int(b * q) + 3

        for p in range(p_min, p_max + 1):
            r = Fraction(p, q)
            if a < float(r) < b:
                found.add(r)

    return sorted(found)


examples = [
    (0.0, 1.0),
    (1.0, 1.001),
    (3.141, 3.142),
]

for a, b in examples:
    rats = rationals_in_interval(a, b, max_denominator=1000)
    print(f"Interval ({a}, {b}) contains {len(rats)} rationals in this search window.")
    print(rats[:10])
    print()
```

The output will show that even very small intervals contain rational numbers.

That is density.

But density is not size.

---

## 2. Enumerate rationals in a bounded window

To connect with measure zero, we need the idea that rationals can be listed.

Here is a simple enumeration of rational numbers in [-1, 1].

```python
def enumerate_rationals(max_denominator=20, lower=-1, upper=1):
    """
    Produce a finite prefix of rationals in [lower, upper].
    Duplicates are removed by using Fraction in lowest terms.
    """
    values = set()

    for q in range(1, max_denominator + 1):
        for p in range(lower * q, upper * q + 1):
            values.add(Fraction(p, q))

    return sorted(values)


rationals = enumerate_rationals(max_denominator=12)
print(len(rationals))
print(rationals[:25])
```

A finite prefix is not the full set ℚ.

But it models the essential fact: ℚ can be organized as a sequence.

q₁, q₂, q₃, ...

That sequence is what makes the measure-zero covering argument possible.

---

## 3. Cover listed rationals with tiny intervals

Given ε > 0, cover the nth rational qₙ with an interval of length:

ε / 2ⁿ

Then the total length is bounded by:

ε/2 + ε/4 + ε/8 + ... = ε

So the whole countable list can be covered with total length less than ε.

Here is the finite computational version.

```python
def rational_cover(rationals, epsilon=0.01):
    """
    Cover the nth rational by an interval centered at that rational
    with length epsilon / 2**n.

    This finite version illustrates the measure-zero covering argument.
    """
    intervals = []

    for n, r in enumerate(rationals, start=1):
        length = epsilon / (2 ** n)
        center = float(r)
        left = center - length / 2
        right = center + length / 2
        intervals.append((left, right, length, r))

    total_length = sum(length for _, _, length, _ in intervals)
    return intervals, total_length


rationals = enumerate_rationals(max_denominator=8)
intervals, total = rational_cover(rationals, epsilon=0.01)

print(f"Number of rationals covered: {len(rationals)}")
print(f"Total interval length used: {total}")
print(f"Target epsilon: 0.01")
print()

for left, right, length, r in intervals[:10]:
    label = str(r).rjust(5)
    print(f"q = {label} covered by ({left:.6f}, {right:.6f}), length = {length:.8f}")
```

The important point is not the specific finite list.

The important point is the pattern.

A countable set can be covered by intervals whose total length is arbitrarily small.

---

## Mathematical takeaway

The rationals ℚ are dense in ℝ:

Every open interval contains rational numbers.

But ℚ has measure zero:

For every ε > 0, ℚ can be covered by countably many intervals whose total length is less than ε.

That is why density and size are different ideas.

Topology sees where a set appears.

Measure theory sees how much size it carries.

The rationals appear everywhere, but carry no length.