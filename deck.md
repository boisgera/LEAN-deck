---
marp: true
theme: default
style: |
  @import url('https://fonts.googleapis.com/css2?family=Fira+Code&display=swap');
  code, pre, kbd {
    font-family: 'Fira Code', monospace !important;
  }
---
<!-- _class: lead -->

<img src="images/lean_logo.svg" width="500" style="display:block;margin:0 auto;">


<p style="text-align:center;"><a href="https://lean-lang.org/">https://lean-lang.org/</a></p>

---
<!-- paginate: true -->

# Lean

Lean is a programming language which manages similarly

- **data types** (`Int`, `String`, `List Float`, ...) and

- **propositions**, (`1 + 1 = 2`, `∀ (n : ℕ), n ≤ 2 ^ n`, `0 = 1 → 1 = 2`, ...)

and there is the same relationship between

- **data** and **data types** (`def answer : ℕ := 42`) and

- **proofs** and **propositions** (`def zero_eq_zero : 0 = 0 := Eq.refl 0`).


---

![bg](<images/Come On What GIF by MOODMAN.gif>)

---

# How does that work concretely?

For example, to define a rational number 

<br>

$$
r = \frac{p}{q} \in \mathbb{Q}
$$


in Lean, you have to provide:

 - 📊 a numerator in $\mathbb{Z}$,
 - 📊 a denominator in $\mathbb{N}$,
 - ✅ a proof that the denominator is not zero,
 - ✅ a proof that the numerator and the denominator are coprime.

💡 Rational numbers are therefore **correct by construction**.

---

# Show me the code!

```lean
structure Rat where
  num : ℤ
  den : ℕ := 1
  den_nz : den ≠ 0 := by decide
  reduced : num.natAbs.Coprime den := by decide

@[inherit_doc] notation "ℚ" => Rat
```

---

# What's the catch?

Lean uses a unfamiliar programming paradigm:

- functional + pure + dependent types

For example:

- Everything is an expression,
- Functions are first-class citizens,
- Types are everywhere,
- Data is immutable,
- There is no implicit side-effects,
- Recursion is fundamental,
- ...

---
<!-- _paginate: false -->
![bg fit](<images/6thsense2.jpg>)

---
<!-- _paginate: false -->
![bg fit](<images/matrix.jpg>)

---
<!-- _paginate: false -->
![bg fit](<images/russell.jpg>)


---
<!-- _paginate: false -->
![bg fit](<images/enlightenment.jpg>)
---


---
<!-- _class: lead -->
<!-- _paginate: false -->
# Appendix I : Formalized Mathematics

What happens when you are only interested in propositions and proofs?

**TODO**: Mathlib, etc.

---
<!-- _class: lead -->
<!-- _paginate: false -->
# Appendix II : Lean and AI

**TODO.** for programs and for Math (ref : FLT)

---
<!-- _class: lead -->
<!-- _paginate: false -->
# Appendix III

---

# 🤖 Softmax

A function $\mathbb{R}^n \to \mathbb{R}^n$, defined by:

<br>

$$
\operatorname{softmax}(x)_i = \frac{\exp x_i}{\sum_{j=1}^n \exp x_j} 
$$

---

# 🐍 Softmax in NumPy

```python
import numpy as np

def softmax(x):
    "Compute the softmax of the NumPy array x"
    y = np.exp(x)
    return y / y.sum()


x = np.array([1.0, 2.0, 3.0])
y = softmax(x)

print(y)
-> array([0.09003057, 0.24472847, 0.66524096])
```

---

# 🐍 Softmax with type hints


```python
import numpy as np
from numpy.typing import NDArray

def softmax(x: NDArray[np.float64]) -> NDArray[np.float64]:
    "Compute the softmax of the NumPy array x"
    y = np.exp(x)
    return y / y.sum()
```

---


Assume that you know only the signature, not the implementation:

<br>

```python
def softmax(x: NDArray[np.float64]) -> NDArray[np.float64]
```

<br>

**What guarantees does Python give you?**

---

![bg fit right:40%](images/this-is-fine-1.png)


# Can `y = softmax(x)`...

- compute incorrect<sup>1</sup> values of `y`?

- accept lists (instead of arrays) of floats?

- raise an exception?

<!-- at bottom of slide -->
<small>1. say with a relative error $> 10^{-12}$.</small>


---

![bg fit right:40%](images/this-is-fine-2.png)


- never return?

- change the value of the input `x`?

- change the value of `np.pi`?


---
![bg fit right:40%](images/this-is-fine-3.png)



- return incorrect values on Monday?

- return incorrect values at random?

- encrypt all your personal files?


---
<!-- _paginate: false -->
![bg fit](images/classes.png)
