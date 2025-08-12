# `TemporalContour`

---

Collection of (frame, row, column) triples corresponding to pixels in a video.

## Initialization

---

> ```py
> def __init__(self, points: list[(int, int, int)]) -> TemporalContour
> ```
> 
> Initializes a `TemporalContour` instance given a set of points.
> `points` should not contain any duplicates.

## Properties

---

> ```py
> @property
> def corners(self) -> ((int, int), (int, int))
> ```
> 
> The top-left and bottom-right of the bounding box containing all points in this contour.


> ```py
> @property
> def frames(self) -> numpy.ndarray
> ```
> 
> The list of frames covered by the points in this contour.


> ```py
> @property
> def height(self) -> int
> ```
> 
> The height of the bounding box containing all the points in this contour.


> ```py
> @property
> def number_of_frames(self) -> ((int, int), (int, int))
> ```
> 
> The total number of frames covered by all the points in the contour.


> ```py
> @property
> def number_of_points(self) -> ((int, int), (int, int))
> ```
> 
> The total number of points in this contour.


> ```py
> @property
> def points(self) -> numpy.ndarray
> ```
> 
> All the points in this contour.


> ```py
> @property
> def region(self) -> View
> ```
> 
> The bounding box containing all the points in this contour.


> ```py
> @property
> def width(self) -> int
> ```
> 
> The width of the bounding box containing all the points in this contour.

## Methods

---

> ```py
> def centroids(self, ndigits: int | None = None) -> list([int, float, float])
> ```
> 
> Frame-by-frame centroid of each 2D contour, returned as a list of (frame, x, y) triples, where `x` and `y` 
> are rounded to `ndigits`.


> ```py
> def crop(
>   src_video: numpy.ndarray,
>   src_level: int,
>   contour_level: int,
>   pad_frames: int | (int, int) = 0
>   pad_region = int | (int, int) | (int, int, int, int) = 0
> ) -> numpy.ndarray
> ```
> 
> Crops the region defined by this contour from `src_video`. The  resolution of the result is the same as the 
> source video, given by `src_level`. This should be a value a greater than or equal to `contour_level`, the 
> resolution of the video that produced the contour.
> 
> See the [`BreatheCam`](/reference/breathecam.md#properties)`.nlevels` property for information about valid 
> sample levels.


> ```py
> def density(ndigits: int | None = None) -> float | int
> ```
> 
> The ratio of the total number of points in this contour to the volume
> of the region containing them rounded to `ndigits`.


> ```py
> def geometric_moments(self, i: int, j: int) -> int
> ```
> 
> Frame-by-frame geometric moment around the point `(i, j)`.


> ```py
> def hu_moments(self, scale: bool = True) -> int
> ```
> 
> Frame-by-frame hu moments, scaling the results when `scale` is `True` (default).


> ```py
> def mask(self, mask_level: int = 1, contour_level: int = 1) -> numpy.ndarray
> ```
> 
> Creates a video mask corresponding to the points in this contour. The 
> resolution of the result is given by `mask_level`. This should be a value a greater than 
> or equal to `contour_level`, the resolution of the video that produced the contour.
> 
> See the [`BreatheCam`](/reference/breathecam.md#properties)`.nlevels` property for information about valid 
> sample levels.


> ```py
> def mask_from(
>   self, 
>   src_video: numpy.ndarray, 
>   src_level: int = 1, 
>   contour_level: int = 1
> ) -> numpy.ndarray
> ```
> 
> Creates a video mask corresponding to the points in this contour, using the
> values of the `src_video` in the mask. The resolution of the result is given by `src_level`. 
> This should be a value a greater than or equal to `contour_level`, the resolution of the 
> video that produced the contour.
> 
> See the [`BreatheCam`](/reference/breathecam.md#properties)`.nlevels` property for information about valid 
> sample levels.


> ```py
> def metadata(self) -> numpy.ndarray
> ```
> 
> A dictionary containing the following keys:
> 
> * `"start_frame": int` - first frame of the contour
> * `"nframes": int` - total number of frames
> * `"npoints": int` - total number of points
> * `"bounding_box": dict` - a dictionary with the region info
>   * `"left": int` - left bound of the box
>   * `"top": int` - top bound of the box
>   * `"right": int` - right bound of the box
>   * `"bottom": int` - bottom bound of the box
>   * `"top_left": (int, int)` - top-left corner of the box
>   * `"bottom_right": (int, int)` - bottom-right corner of the box
>   * `"height": int` - height of the box
>   * `"width": int` - width of the box


> ```py
> def points_by_frame(self) -> dict[int, numpy.ndarray]
> ```
> 
> The points in the contour organized by frame.


> ```py
> def save(
>   path: str,
>   src_video: numpy.ndarray,
>   src_level: int,
>   contour_level: int,
>   pad_frames: int | (int, int) = 0
>   pad_region = int | (int, int) | (int, int, int, int) = 0
> )
> ```
> 
> Crops the region defined by the contour from `src_video` and exports it to
> to `path`. Where the path is a `.mp4` filename. The resolution of the result is the same 
> as the source video, given by `src_level`. This should be a value a greater than or equal 
> to `contour_level`, the resolution of the video that produced the contour.
> 
> See the [`BreatheCam.nlevels`](/reference/breathecam.md) property for information about 
> valid sample levels.