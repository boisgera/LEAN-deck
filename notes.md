
$$
x\in \mathbb{R}^n
$$

$$
\operatorname{softmax} : \mathbb{R}^n \to \mathbb{R}^n
$$

$$
\operatorname{softmax}(x)_i = \frac{\exp x_i}{\sum_j=i^n \exp x_j}
$$


```python
import numpy as np

def softmax(x):
    y = np.exp(x)
    return y / y.sum()
```

```pycon
>>> x = np.array([1.0, 2.0, 3.0])
>>> softmax(x)
array([0.09003057, 0.24472847, 0.66524096])
```

```python
import numpy as np
from numpy.typing import NDArray

def softmax(x: NDArray[np.float64]) -> NDArray[np.float64]:
    y = np.exp(x)
    return y / y.sum()
```

Now assume that you know only the signature:

```python
def softmax(x: NDArray[np.float64]) -> NDArray[np.float64]:
    ...
```

Can an implementation with this signature

- [ ] compute values that are very different from our expectation?

- [ ] return an array with a shape different from the shape of `x`?

- [ ] accept lists (and not arrays) of floats?

- [ ] raise an exception?

- [ ] change the value of the input `x`?


-----

- [ ] return wrong values unless your OS is Linux?

- [ ] return a wrong value 0.01% of the time?

- [ ] change the value of $\pi$ to `3.0`?


----

- [ ] compute until the end of the universe ? 

- [ ] say out loud "Alexa, order 1000 rolls of toilet papers"?

- [ ] encrypt all the files in your home directory?


----

Python is

- imperative + object-oriented + some functional bits
- interpreted
- dynamically / gradually typed


----

Lean is

- a pure functional programming language
- statically type-checked + compiled
- with a very expressive type system

-----

```lean
structure Rat where
  /-- The numerator of the rational number is an integer. -/
  num : Int
  /-- The denominator of the rational number is a natural number. -/
  den : Nat := 1
  /-- The denominator is nonzero. -/
  den_nz : den ≠ 0 := by decide
  /-- The numerator and denominator are coprime: it is in "reduced form". -/
  reduced : num.natAbs.Coprime den := by decide
```