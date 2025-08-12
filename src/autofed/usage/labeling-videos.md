# Labeling Videos

---

Once videos have been generated, they can be inserted into a database for labeling. We will be leveraging methods in
 the [`AutoFEDDB`](/reference/autofed-db.md) class.

```python
from autofed import AutoFEDDB
```

First we define classication options or labels. These will be applied to each video in the set.

```python
classification_options = ["smoke","steam", "shadow", "other_motion", "none"]
```

Now we can start the database and insert the videos. Ensure that a database with the given name exists and is 
accessible.

```python
adb = AutoFEDDB("smoke-detect", classification_options)

html_file = "/.../.../.../events_13626_frames_20250303_065000_1.html"
run_name = os.path.splitext(os.path.basename(html_file))[0]

adb.insert_from_html(
  table="generated-videos", 
  run=run_name, 
  html_file=html_file
)
```

Now when we run the `labeler` application we should see a page similar to:

![labeling-app-front-page](/autofed/assets/app-homepage.png)

Clicking on the link opens a page of videos.

![labeling-app-videos](/autofed/assets/app-scroll.png)

Video labels are automatically persisted to the database in a table called `"video-labels"`.