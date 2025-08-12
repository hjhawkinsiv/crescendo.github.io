# `DoubleExponentialSmoother`

---

Implements double exponential smoothing.

\\[
\begin{align*}
  L_n &= \alpha d_n + (1 - \alpha)(L_{n - 1} + T_{n - 1}), ~~~ 0 \le \alpha \le 1\\\\[1em]
  T_n &= \gamma (L_n - L_{n - 1}) + (1 - \gamma)T_{n - 1}, ~~~ 0 \le \gamma \le 1
\end{align*}
\\]

Smoothing works by updating a *level* and *trend* component using smoothing factors *alpha* (\\(\alpha\\)) 
and *gamma* (\\(\gamma\\)), where \\(\alpha\\) controls the smoothing of the level component and 
\\(\gamma\\) controls the smoothing of the trend component. The higher the alpha the more weight that is 
given to recent data.


## Initialization

---

> ```py
> def __init__(
>   self, 
>   level: numpy.ndarray, 
>   trend: numpy.ndarray, 
>   alpha: float, 
>   gamma: float | None = None
> ) -> DoubleExponentialSmoother
> ```
> 
> Initializes a `DoubleExponentialSmoother` with starting `level`, `trend`, and smoothing factors `alpha` and `gamma`. 
> When `gamma` is None, the returned smoother is equivalent to a Browns double exponential smoother, where
> `gamma = alpha / (1 - alpha)`.
> 


## Properties

---

```py
@property
def alpha(self) -> numpy.ndarray
```

> The level smoothing factor

```py
@property
def gamma(self) -> numpy.ndarray
```

> The trend smoothing factor


```py
@property
def level(self) -> numpy.ndarray
```

> The current level data


```py
@property
def trend(self) -> numpy.ndarray
```

> The current trend data


## Methods

---

```py
def update(self, data: numpy.ndarray) -> (numpy.ndarray, numpy.ndarray)
```

> Updates and returns the `level` and `trend` of the smoother with `data`.