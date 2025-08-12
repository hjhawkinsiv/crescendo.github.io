# Downloading Videos

---

```python
from autofed import BreatheCam
```

We initialize access to the BreatheCam data for Clairton Coke Works on May 19th, 2024.

```python
location = "Clairton Coke Works"
day = "2024-05-19"
breathecam = BreatheCam.init_from(location, day)
```
This will allow us to download video for any point during this day. Note, this camera records frames a rate of 3 
seconds per frame, for example, 10 frames is 30 seconds of footage. Now we set up the range of time we want to
download. In this case, it is an hour an a half (90 seconds) of footage starting at 9:49 in the morning.

```
start_time = "09:49:00"
end_time = "11:19:00"
start_frame = breathecam.capture_time_to_frame(start_time)
end_frame = breathecam.capture_time_to_frame(end_time)
nframes = end_frame - start_frame // does not include frame starting at 11:19:00
```

The last two values to set up is the bounding box, a portion of the camera's view to capture, and the resolution level.
Both of these values influence the amount of time the download will take. The larger the view and the higher the level,
the longer it takes. `downsampled` is the video downsampled by 4. It is a fourth of the size of the full resolution
video, where `nlevels=1`

```
nlevels = 4
view = View(2307, 1914, 6814, 2515)
downsampled_video = breathecam.download_video(start_frame, nframes, view, nlevels)
full_resolution_video = breathecam.extract(start_brame, nframes, view, 1)
```