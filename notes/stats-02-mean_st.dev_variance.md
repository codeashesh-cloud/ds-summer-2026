# Stats 02 — Variance and Standard Deviation

## Why we need them

The **mean** tells us the *center* of the data.
But two datasets can have the **same mean** with very different *spreads*.

**Example:**
- Dataset A: `[48, 49, 50, 51, 52]` → mean = 50, tightly clustered
- Dataset B: `[10, 30, 50, 70, 90]` → mean = 50, widely spread

Same mean, completely different stories. We need a way to measure **spread** — that's variance and standard deviation.

---

## Step-by-step: how variance is calculated

For a dataset `[2, 4, 4, 4, 5, 5, 7, 9]`:

**Step 1 — Find the mean.**
mean = (2+4+4+4+5+5+7+9) / 8 = **5**

**Step 2 — Find each value's distance from the mean.**
2−5 = −3
4−5 = −1
4−5 = −1
4−5 = −1
5−5 = 0
5−5 = 0
7−5 = 2
9−5 = 4

**Step 3 — Square each distance.**
9, 1, 1, 1, 0, 0, 4, 16

(Why square? See below.)

**Step 4 — Average the squared distances.**
(9+1+1+1+0+0+4+16) / 8 = 32/8 = **4**

That's the **variance** = 4.

**Step 5 — Take the square root to get standard deviation.**
√4 = **2**

That's the **standard deviation** = 2.

---

## The 4 key questions

### 1. Why do we need variance/std dev?

To measure **how spread out** the data is around the mean. The mean alone hides this information.

### 2. Why do we SQUARE the differences?

Because if we just added `(x − mean)`, the **positives and negatives would cancel out** and we'd always get zero — useless.

Squaring forces every difference to be positive so they accumulate instead of cancelling.

### 3. What's the relationship between variance and standard deviation?

```
standard deviation = √variance
variance = (standard deviation)²
```

They measure the same thing — just in different units.

### 4. Why is standard deviation more useful than variance?

**Units.**

If your data is in centimeters:
- Variance is in **cm²** (squared centimeters — meaningless to humans)
- Std dev is in **cm** (same units as your data — easy to interpret)

So we report std dev in plain English:
> *"On average, values are about [std dev] away from the mean."*

---

## Intuition: what std dev tells you

If a class has:
- Mean exam score = **75**
- Std dev = **8**

Then most students scored roughly between **67 and 83** (75 ± 8).

**Comparing two datasets with same mean:**

| Class | Mean | Std Dev | What it means |
|-------|------|---------|---------------|
| A | 80 | 3 | Tight cluster — everyone scored close to 80 |
| B | 80 | 15 | Wide spread — scores all over the place |

---

## Special cases to remember

- If **all values are identical** (e.g. `[5, 5, 5, 5, 5]`), variance = 0 and std dev = 0. There's no spread.
- Std dev is **never negative** (it's a square root of a non-negative number).
- Larger std dev = more spread = more variability.

---

## Quick reference table

| Term | What it is | Units | Use |
|------|------------|-------|-----|
| Mean | Center of the data | Same as data | Where the data sits |
| Variance | Average of squared distances from mean | Squared units | Math-friendly measure of spread |
| Std Dev | √Variance | Same as data | Human-friendly measure of spread |

---

## Memory hooks

- **Mean** = center
- **Variance** = "how far on average, but squared"
- **Std dev** = "how far on average, in real units"
- Squaring fixes the negatives-cancelling-positives problem
- Std dev is what you actually **report** to people