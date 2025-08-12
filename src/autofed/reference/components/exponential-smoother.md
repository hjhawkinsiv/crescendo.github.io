# `ExponentialSmoother`

---

Implements single exponential smoothing.
    
\\[
\begin{align*}
  L_n &= \alpha d_n + (1 - \alpha)(L_{n - 1}), ~~~ 0 \le \alpha \le 1
\end{align*}
\\]

Smoothing works by updating a *level* component using a smoothing factor *alpha* \\(\alpha\\). Where alpha controls 
the smoothing of the level component. The higher the alpha the more weight that is given to recent data. 


## Initialization

---

```py
def __init__(self, level: numpy.ndarray, alpha: float) -> ExponentialSmoother
```

> Initializes an `ExponentialSmoother` with the starting `level` and smoothing factor `alpha`.


## Properties

---

```py
@property
def alpha(self) -> numpy.ndarray
```

> The level smoothing factor



```py
@property
def level(self) -> numpy.ndarray
```

> The current level data


## Methods

---

```py
def update(self, data: numpy.ndarray) -> numpy.ndarray
```

> Updates and returns the `level` of the smoother with `data`.