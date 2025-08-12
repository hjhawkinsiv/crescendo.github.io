# `ElementLibrary`

---

Defines a type that treats a class as a dictionary with class variable names as keys.

> ```python
> class Elements(metaclass=ElementLibrary):
>    LabeledDivs = "div.labeled"
>
> labeled_divs = Elements["LabeledDivs"]
>```
