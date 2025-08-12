# `DisjointSet[T]`

---

Implements a union-find data structure.


## Initialization

---

> ```py
> def __init__(self) -> DisjointSet
> ```
> 
> Initializes an empty `DisjointSet`.


## Methods

---

> ```py
> def add(self, element: T):
> ```
> 
> Adds `element` to the set if it's not already there, compressing the path from
> the root of the set to which it belongs to the element itself. If `element` is 
> missing, then a new subset is added with the element at the root.

> ```py
> def find(self, element: T) -> T:
> ```
> 
> Adds `element` to the set if it's not already there, compressing the path from
> the root of the set to which it belongs to the element itself. If `element` is 
> missing, then a new subset is added with the element at the root. In either case,
> the root is returned.


> ```py
> def union(self, x: T, y: T):
> ```
> 
> Merges the two subsets containing `x` and `y` if they do not already belong to
> the same set.