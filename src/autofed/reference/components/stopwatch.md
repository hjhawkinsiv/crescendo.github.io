# `Stopwatch`

---

Implements a timer.

## Initialization

---

> ```py
> def __init__(self, name: str, print_stats: bool = True) -> Stopwatch
> ```
> 
> Initializes a `Stopwatch` with `name` as its identifier, optionally
> printing a stats message when stopped.


## Properties

---

> ```py
> @property
> def name(self) -> str
> ```
> 
> The identifier of the stopwatch.


> ```py
> @property
> def print_stats(self) -> str
> ```
> 
> Whether to print a stats message when the stopwatch is stopped.


> ```py
> @property
> def stats_message(self) -> str
> ```
> 
> The stats message printed when the stopwatch is stopped
> if `print_stats` is true.


## Methods

---

> ```py
> def cpu_elapsed(self) -> float
> ```
> 
> Number of process seconds that have elapsed.


```py
def set_stats_message(self, message: str)
```

> Updates the stats message to be printed when the stopwatch is stopped.


```py
def start(self)
```

> Starts the stopwatch.


```py
def stop(self)
```

> Stops the stopwatch, optionally printing a stats message.


```py
def wall_elapsed(self) -> float
```

> Number of wall clock seconds that have elapsed.


## Context Management


```py
def __enter__(self) -> Stopwatch
```

> Starts a stopwatch context

```py
def __exit__(self, type, value, traceback)
```

> Ends a stopwatch context, optionally printing a stats message.