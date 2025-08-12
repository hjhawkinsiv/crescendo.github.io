# `BreatheCam`

---

Implements a wrapper around a BreatheCam, a high-resolution, 24-hour live camera feed trained 
on an industrial pollution source in Pennsylvania.

## Currently Available Cameras

---

This list does not reflect all cameras available on [breathecam.org](https://breathecam.org).

```py
from breathecam import CAMERAS
```

|             Name                                   |      Id     |
|----------------------------------------------------|:-----------:|
|   Clairton Coke Works                              | clairton4
|   Shell Plastics West                              | vanport3
|   Edgar Thomson South                              | westmifflin2
|   Metalico                                         | accan2
|   Revolution ETC/Harmon Creek Gas Processing Plants| cryocam
|   Riverside Concrete                               | cementcam
|   Shell Plastics East                              | center1
|   Irvin                                            | irvin1
|   North Shore                                      | heinz
|   Mon. Valley                                      | walnuttowers1
|   Downtown                                         | trimont1
|   Oakland                                          | oakland



## Initialization

---

> ```py
> def __init__(
>   self,
>   location: str, 
>   day: datetime.date | str, 
>   *, 
>   date_formatter: (str -> datetime.date) | None = None
> ) -> BreatheCam
> ```
> 
> Initializes a `BreatheCam` instance given a `location` and `day`.
> If `day` is a string and not in ISO format ("*YYYY-MM-DD*"), then 
> a `date_formatter` should be provided.
>
> `location` must be a name or id in the list of available cameras above.
> 
> ```py
> camera = BreatheCam("Clairton Coke Works", "2024-05-19")
> ```

## Static Methods

---

> ```py
> @staticmethod
> def download(
>   location: str, 
>   day: datetime.date,
>   time: datetime.time,
>   bbox: BoundingBox | None = None,
>   nframes: int = 1,
>   level: int = 1
> ) -> numpy.ndarray
> ```
> 
> Downloads `nframes` of the region defined by `bbox` for the BreatheCam 
> at `location` for the given `day` and `time`. The resolution of the
> video is determined by `level`, which should be a value in `{1, 2, 4, 8}`.
> `level = 1` downloads the video at full resolution.
> 
> ```py
> video = BreatheCam.download(
>   "Clairton Coke Works", 
>   datetime.date.fromisoformat("2024-05-19"),
>   datetime.time.fromisoformat("09:49:00"),
>   bbox=BoundingBox(4554, 2027, 5015, 2422),
>   nframes=60
>   nlevels=4
> )
> ```

## Properties

---

> ```py
> @property
> def capture_times(self) -> list[str]
> ```
> 
> List of times captured by this `BreatheCam`. Each element of the
> returned list is a date and time formatted as "*YYYY-MM-DD hh::mm::ss*"
> 
> ```py
> camera = BreatheCam("Clairton Coke Works", "2024-05-19")
> capture_times = camera.capture_times
> 
> print(capture_times[0]) # '2025-07-16 00:00:00'
> print(capture_times[1]) # '2025-07-16 00:00:03'
> ```


> ```py
> @property
> def day(self) -> str
> ```
> 
> The calendar day corresponding to the metadata of this `BreatheCam`.
> 
> ```py
> camera = BreatheCam("Clairton Coke Works", "2024-05-19")
> print(camera.day) # 2024-05-19
> ```


> ```py
> @property
> def fps(self) -> float
> ```
> 
> Frames per second for this `BreatheCam`.
> 
> ```py
> camera = BreatheCam("Clairton Coke Works", "2024-05-19")
> 
> print(camera.fps) # 12.0
> ```


> ```py
> @property
> def nlevels(self) -> int
> ```
> 
> The number of sampling levels available for this `BreatheCam`.
>
> For a given `nlevels`, the corresponding sample levels come from the list
> [2<sup>i</sup> for i in 0..(`nlevels` - 1)].
> 
> ```py
> camera = BreatheCam("Clairton Coke Works", "2024-05-19")
> 
> print(camera.nlevels) # 4
> ```

## Methods

---

> ```py
> def capture_time_to_frame(self, time: datetime.time | str) -> int
> ```
> 
> Gets the frame index for the given `time`. If `time` is a string 
> and not in ISO format ("*hh:mm:ss*"), then a `time_formatter` should 
> be provided.
> 
> ```py
> camera = BreatheCam("Clairton Coke Works", "2024-05-19")
> 
> print(camera.capture_time_to_frame("09:49:00")) # 11776
> ```


> ```py
> def extract(
>   self,
>   time: datetime.time,
>   bbox: BoundingBox | None = None,
>   nframes: int = 1,
>   level: int = 1
> ) -> numpy.ndarray
> ```
> 
> Downloads `nframes` of the region defined by `bbox` for this `BreatheCam` 
> for the given `time`. The resolution of the video is determined by `level`,
> where `level = 1` downloads the video at full resolution. `level` should
> be a power of 2 greater than 0 and less than the 2<sup>`self.nlevels` - 1</sup>.
> 
> ```py
> camera = BreatheCam("Clairton Coke Works", "2024-05-19")
> 
> video = camera.extract(
>   datetime.time.fromisoformat("09:49:00"),
>   bbox=BoundingBox(4554, 2027, 5015, 2422),
>   nframes=60
>   nlevels=4
> )
> ```

> ```py
> def height(self, level: int = 1) -> int
> ```
> 
> Height of the video sampled at `level`, where `level = 1` is the height of the 
> full resolution video. `level` should be a power of 2 greater than 0 and less 
> than the 2<sup>nlevels - 1</sup>.
> 
> ```py
> camera = BreatheCam("Clairton Coke Works", "2024-05-19")
> 
> print(camera.height())  # 2792
> print(camera.height(2)) # 1396
> print(camera.height(4)) # 698
> print(camera.height(8)) # 349
> ```


> ```py
> def width(self, level: int = 1) -> int
> ```
> 
> Width of the video sampled at `level`, where `level = 1` is the width of the 
> full resolution video. `level` should be a power of 2 greater than 0 and less 
> than the 2<sup>nlevels - 1</sup>.
> 
> ```py
> camera = BreatheCam("Clairton Coke Works", "2024-05-19")
> 
> print(camera.width())  # 7908
> print(camera.width(2)) # 3954
> print(camera.width(4)) # 1977
> print(camera.width(8)) # 989
> ```