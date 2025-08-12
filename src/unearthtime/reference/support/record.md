# `Record[T]`

---

Implements an immutable `dict[str, T]` type. Trying to mutate the dictionary after initialization causes an 
exception. While a record itself cannot be modified, the value pointed to by a key may still be able to
be mutated. 

```python
record = Record({"x": []})

print(record["x"]) # []

record["x"].append(1)

print(record["x"]) # [1]
```

It is recommended that values be immutable, otherwise, care should be taken that none of them are changed.

## Initialization 

---

> ```python
> def __init__(
>   map_or_iter: Mapping[str, T] | Iterable[(str, T)] | None = None,
>   **kwargs
> ) -> Record[T]
> ```
>
> Initializes a record with the key-value pairs from `map_or_iter`. If `map_or_iter` is `None` then the 
> returned record is empty.
>
> ```python
> empty = Record()
>
> print(len(empty)) # 0
>
> record = Record({"x": 1, "y": 2, "z": 3})
>
> print(record["x"]) # 1
> ```

## Methods

> ```python
> copy(self) -> Record[T]
> ```
> 
> Shallow copy of a record.
>
> ```python
> record = Record({"x": 1, "y": 2, "z": 3})
> copy = record.copy()
> ```

> ```python
> __eq__(self, other: Record[T]) -> bool
> ```
> 
> Whether two records are equal.
>
> ```python
> record = Record({"x": 1, "y": 2, "z": 3})
> 
> print(record == record.copy()) # True
>
> other_record = Record({"x": 1, "y": 2, "z": 0})
>
> print(record == other_record) # False
>
> another_record = Record({"x": "1", "y": "2", "z": "3"})
>
> print(record == another_record) # False
> ```

> ```python
> __ne__(self, other: Record[T]) -> bool
> ```
> 
> Whether two records are equal.
>
> ```python
> record = Record({"x": 1, "y": 2, "z": 3})
> 
> print(record != record.copy()) # False
>
> other_record = Record({"x": 1, "y": 2, "z": 0})
>
> print(record != other_record) # True
>
> another_record = Record({"x": "1", "y": "2", "z": "3"})
>
> print(record != another_record) # True
> ```