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

# LEAN

---
<!-- paginate: true -->


# LEAN 4

- functional + pure
- dependently typed

+ programming language 
+ proof assistant

---

# $\Large{\pi}$/🤖 Softmax

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
    y = np.exp(x)
    return y / y.sum()
```

---

Assume that you know only the signature:

<br>

```python
def softmax(x: NDArray[np.float64]) -> NDArray[np.float64]
```

<br>

**What guarantees do you have?**

---

![bg fit right:33%](images/this-is-fine-1.png)


# Can `y = softmax(x)`...


- compute "incorrect" values of `y`?

- accept lists (instead of arrays) of floats?

- raise an exception?


---

![bg fit right:33%](images/this-is-fine-1.png)


- never return?

- change the value of the input `x`?

- change the value of `np.pi`?


---
![bg fit right:33%](images/this-is-fine-1.png)



- return incorrect values if your OS is Windows?

- return incorrect values 0.01% of the time?

- encrypt all the files in your home directory?


---
<!-- _paginate: false -->
![bg fit](images/classes.png)

---