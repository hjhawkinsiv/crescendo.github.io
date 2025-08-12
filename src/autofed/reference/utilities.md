# `utilities`

---

Implements various helper methods.


## Methods

---

> ```py
> def backtrack(time: datetime.time, seconds: int) -> datetime.time
> ```
> Steps `time` back a number of seconds


> ```py
> def coords2D_in_radius(radius: float, point: (int, int), matrix: numpy.ndarray)
> ```
> 
> Draws a circle around a point in a matrix and returns all indices within it.

> ```py
> def coords3D_in_radius(radius: int, point: (int, int, int), matrix: numpy.ndarray)
> ```
> 
> Draws a sphere around a `point` in a matrix and returns all indices within `radius`.


> ```py
> def export_contours_to_html(
>     html_path: str,
>     videos_dir: str,
>     contours: list[TemporalContour],
>     src: numpy.ndarray, 
>     src_nlevels: int,
>     contour_nlevels: int,
>     pad_frames: FramePadding = 0,
>     pad_region: PixelPadding = 0,
>     title: str = "",
>     video_file_prefix: str = "event"
> )
> ```
> 
> Exports videos to the html page `html_path`. Each contour in `contours` is cropped from the `src` video
> and optionally padded with extra frames and/or space. Videos are stored in `videos_dir` each named, where, 
> `contours[i]` generates the file "{`videos_dir`}/{`video_file_prefix`}_{`i` + 1}". 
> `title` will appear at the top of the page.
    

> ```py
> def export_to_mp4(path: str, video: numpy.ndarray)
> ```
> 
> Exports `video` as an mp4 to `path`.


> ```py
> def gaussian_kernel(npoints: int, std_dev: float) -> numpy.ndarray
> ```
> 
> Generates a kernel based on a gaussian distribution defined
> by a window with `npoints` and a sigma of `std_dev`.



> ```py
> def get_frame_time(time: datetime.time, seconds_per_frame: int) -> datetime.time
> ```
> 
> Adjusts `time` to match an offset representing the start of a frame, where each frame
> is `seconds_per_frame` long.


> ```py
> def get_previous_frame_time(
>     time: datetime.time, 
>     seconds_per_frame: int, 
>     nframes: int = 1
> ) -> datetime.time
> ```
> 
> Adjusts `time` to match an offset representing the start of the frame `nframes` away from the current one
> where each frame is `seconds_per_frame` long.