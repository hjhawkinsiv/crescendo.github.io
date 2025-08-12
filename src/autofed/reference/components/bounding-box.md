# `BoundingBox`

---

Implements a bounded or rectangular region.

## Initialization

---

> ```py
> def __init__(self, left: int, top: int, right: int, bottom: int ) -> BoundingBox
> ```
> 
> Initializes a `BoundingBox` defined by the corners (`top`, `left`) and (`bottom`, `right`)
> 
> ```py
> print(BoundingBox(2307, 1914, 6814, 2515)) 
> # BoundingBox(left=2307, top=1914, right=6814, bottom=2515)
> ```


## Properties

---

> ```py
> @property
> def bounds(self) -> (int, int, int, int)
> ```
> 
> The left, top, right, and bottom bounds.
>
> ```py
> bbox = BoundingBox(2307, 1914, 6814, 2515)
> 
> print(bbox.bounds)  
> # (2307, 1914, 6814, 2515)
> ```

> ```py
> @property
> def height(self) -> int
> ```
> 
> Height of the bbox.
> 
> ```py
> bbox = BoundingBox(2307, 1914, 6814, 2515)
> 
> print(bbox.height())  # 601
> ```


> ```py
> @property
> def width(self) -> int
> ```
> 
> Width of the bbox.
> 
> ```py
> bbox = BoundingBox(2307, 1914, 6814, 2515)
> 
> print(bbox.width()))  # 4507
> ```


## Methods

---

> ```py
> def center(self) -> (int, int)
> ```
> 
> The center point of the bbox in (row, column) format.
>
> ```py
> bbox = BoundingBox(2307, 1914, 6814, 2515)
> 
> print(bbox.center())  # (2553, 300)
> ```


> ```py
> def intersection(self, other: BoundingBox) -> BoundingBox | None
> ```
> 
> The intersection of two bboxs if it exists.
>
> ```py
> bbox1 = BoundingBox.full(3000, 0, 7930, 2515)
> bbox2 = BoundingBox(2307, 1914, 6814, 2808)
> 
> print(bbox1.intersection(bbox2))  
> # BoundingBox(left=3000, top=1914, right=6814, bottom=2515)
> ```


> ```py
> def scaled_down(self, scale: int | float) -> BoundingBox
> ```
> 
> Divides each bound by `scale`.
>
> ```py
> bbox = BoundingBox(2307, 1914, 6814, 2515)
> 
> print(bbox.scaled_down(2))  
> # BoundingBox(left=1154, top=957, right=3407, bottom=1258)
> ```


> ```py
> def scaled_up(self, scale: int | float) -> BoundingBox
> ```
> 
> Multiplies each bound by `scale`.
>
> ```py
> bbox = BoundingBox(2307, 1914, 6814, 2515)
> 
> print(bbox.scaled_up(2))  
> # BoundingBox(left=4614, top=3828, right=13628, bottom=5030)
> ```

> ```py
> def translated(self, dx: int, dy: int) -> BoundingBox
> ```
> 
> Shifts the left and right by `dx`, and the top and bottom by `dy`.
> The bounds of the returned `BoundingBox` are 
> (left - dx, top - dy, right + dx, bottom + dy). When `dx` is greater 
> than 0, the box is stretched horizontally. When `dy` is greater than 
> 0, the box is stretched vertically. 
>
> ```py
> bbox = BoundingBox(2300, 1900, 6800, 2500)
> 
> print(bbox.translated(128, 128))
> # BoundingBox(left=2172, top=1772, right=6928, bottom=2628)
>
> print(bbox.translated(128, -128))
> # BoundingBox(left=2172, top=2028, right=6928, bottom=2372)
>
> print(bbox.translated(-128, 128))
> # BoundingBox(left=2428, top=1772, right=6672, bottom=2628)
>
> print(bbox.translated(-128, -128))
> # BoundingBox(left=2428, top=2028, right=6672, bottom=2372)
> ```