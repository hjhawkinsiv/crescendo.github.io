# `AutoFEDDB`

---

Wraps a database for maintaining and persisting temporal events and associated classifications.

## Metadata

Each video in the database is stored as a dictionary with the following keys:
* `"record_id": str` -- the id of the video in the table
* `"index": int` -- the index of the video in the run that produced it
* `"source": str` -- source of the video used for labeling
* `"start_frame": int` -- the starting frame of this video in the one used for extraction
* `"nframes": int` -- the length of the video in frames
* `"classifications": list[str]` -- the labels applied to the video
* `"bounding_box": dict` -- bounding box of this video in the one used for extraction, with keys:
  * `"left": int` - left bound of the box
  * `"top": int` - top bound of the box
  * `"right": int` - right bound of the box
  * `"bottom": int` - bottom bound of the box
  * `"top_left": (int, int)` - top-left corner of the box
  * `"bottom_right": (int, int)` - bottom-right corner of the box
  * `"height": int` - height of the box
  * `"width": int` - width of the box


## Initialization

---

> ```py
> def __init__(self, name: str, classification_options: Iterable[str]) -> AutoFEDDB
> ```
> 
> Creates a connection to the database `dbname` of temporal events labeled by the given `classification_options`.


## Properties

---

> ```py
> @property
> def classification_options(self) -> tuple[str...]
> ```
> 
> The labels to choose from for each event.


> ```py
> @property
> def name(self) -> str
> ```
> 
> The name of the database.


## Methods

---

> ```py
> def all_videos_for_run(self, table: str, run: str) -> list[dict[str]]
> ```
> 
> Gets the metadata for all videos in `table` with the given `run` name. See the [metadata](#metadata) section
> for details about what information each dictionary contains.


> ```py
> def available_runs(self, table: str)
> ```
> 
> List of run names in `table`.


> ```py
> def close(self)
> ```
> 
> Closes the connection to the database.


> ```py
> def create_table(self, name: str)
> ```
> 
> Creates a table in the database with the given `name`.


> ```py
> def delete_run(self, table: str, run: str)
> ```
> 
> Deletes the data associated with `run` from the given `table`.


> ```py
> def drop_table(self, table: str)
> ```
> 
> Deletes the data associated with the given `table` from the database.


> ```py
> def insert(self, table: str, data: dict[str])
> ```
> 
> Inserts `data` into the given `table`.
>
> `data` is a dictionary with the keys:
> * `"run_name": str` -- the name of the run that produced the data
> * `"video_src": str` -- the source of the video for labeling
> * `"metadata": str` -- a parsable string of extra information
>
> `data["metadata"]` is parsed into a portion of the overall [metadata](#metadata) dictionaries returned
> by `all_videos_for_run`.

> ```py
> def insert_from_html(self, table: str, html_file: str, video_container_class: str = "video-container")
> ```
> 
> Inserts `data` into the given `table` parsed from a `html_file`. Each video in the file is expected to be formatted
> as 
> 
>```html
> <div class="video-container">
>   <video src="..."></video>
>   <div class="metadata">...</div>
> </div>
> ```
> 
> [`utilities`](/reference/utilities.md)`.export_contours_to_html` is available for generating HTML files parsable
> by this method from [temporal contours](/reference/temporal-contour.md).


> ```py
> def labeled_videos_for_run(self, run: str, classification_filter: list[string] -> bool) -> list[dict[str]]
> ```
> 
> Gets the metadata for all videos with the given `run` name and classifications for which `classification_filter`
> return true. See the [metadata](#metadata) section for details about what information each dictionary contains.


> ```py
> def insert_from_html(self, table: str, html_file: str, video_container_class: str = "video-container")
> ```
> 
> Inserts `data` into the given `table` parsed from a `html_file`. Each video in the file is expected to be formatted
> as 
> 
>```html
> <div class="video-container">
>   <video src="..."></video>
>   <div class="metadata">...</div>
> </div>
> ```
> 
> [`utilities`](/reference/utilities.md)`.export_contours_to_html` is available for generating HTML files parsable
> by this method from [temporal contours](/reference/temporal-contour.md).


## Context Management


```py
def __enter__(self) -> AutoFEDDB
```

> Starts a connection to a database.

```py
def __exit__(self, type, value, traceback)
```

> Closes the connection to the dabase.