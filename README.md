Here is the intelligent translation of the provided **`README.md`** focusing on using **RTSP video streams** (from IP cameras) instead of `.mp4` video files:

---

```md
# Core_process Documentation

The `Core_process` class is used in this project for real-time object detection and tracking from **IP camera streams** using the **RTSP protocol**, based on the **YOLOv8** model and **DeepSort** tracker. It enables the detection of objects, tracking of individuals, and monitoring of intrusions within a defined time window.

## Table of Contents

1. [Role of the `Core_process` class](#role-of-the-core_process-class)
2. [Flexible instantiation with default values](#flexible-instantiation-with-default-values)
3. [Method Descriptions](#method-descriptions)
4. [Key Method Details](#key-method-details)
    - [process_video](#process_video)
    - [is_intrusion](#is_intrusion)
    - [plot_boxes](#plot_boxes)
5. [Usage Example](#usage-example)

---

## Role of the `Core_process` class

The **`Core_process`** class is the core component of this project. It manages:
- **Object detection** in real-time video streams from **IP cameras** using the **RTSP protocol**.
- **Object tracking** using **DeepSort**.
- **Intrusion detection** within a predefined time range.

This class leverages the **YOLOv8** model for real-time detections and displays the detected objects with bounding boxes. It also allows dynamic configuration of parameters such as the **confidence threshold**, **person-only detection**, and intrusion time windows.

## Flexible instantiation with default values

Some parameters in the class have default values, making it easy to **instantiate** by simply providing the RTSP URL of the IP camera.

Example of a simple instantiation (with default values):

```python
detector = Core_process(capture="rtsp://192.168.1.100:554/stream1")
```

However, you can customize these values during instantiation if needed:

```python
detector = Core_process(capture="rtsp://192.168.1.100:554/stream1", confidence_threshold=0.6, person_only=True, start_hour=20, end_hour=6)
```

### Default parameters and customization:

- **`confidence_threshold`**: Default is `0.5`, used to filter out objects with lower confidence.
- **`person_only`**: Default is `False`. When set to `True`, only people will be detected.
- **`start_hour` and `end_hour`**: Define the time window during which intrusions are monitored (default: 11 PM to 5 AM).

## Method Descriptions

### 1. `__init__`
```python
def __init__(self, capture, confidence_threshold=0.5, person_only=False, start_hour=23, end_hour=5):
```
- **Parameters**:
  - **`capture`**: RTSP URL of the IP camera (e.g., `"rtsp://192.168.1.100:554/stream1"`).
  - **`confidence_threshold`**: Confidence threshold for filtering objects (default: `0.5`).
  - **`person_only`**: If `True`, only people will be detected (default: `False`).
  - **`start_hour`** and **`end_hour`**: Time window to check for intrusions (default: 11 PM to 5 AM).

### 2. `load_model`
Loads and optimizes the YOLO model for object detection.

### 3. `set_confidence_threshold`
Dynamically adjusts the **confidence threshold** for object detection.

### 4. `set_person_only`
Enables or disables person-only detection.

### 5. `predict`
Runs object detection on a given image or frame.

### 6. `plot_boxes`
Draws **bounding boxes** around detected objects and displays the number of detections on the image.

### 7. `track_detect`
Performs **object tracking** using **DeepSort** on detected objects.

### 8. `is_intrusion`
Checks whether an **intrusion** has been detected within the defined time window.

### 9. `process_video`
Processes the RTSP video stream and applies object detection, tracking, and intrusion verification.

---

## Key Method Details

### `process_video`

This method is the main one for handling video streams. It takes an RTSP URL, captures each frame from the IP camera, applies detection using YOLO, draws bounding boxes, applies object tracking using DeepSort, and checks for **intrusions** based on the defined time window.

- **Returns**: A generator that yields for each frame:
  - The annotated frame with detected objects.
  - The total number of detected objects.
  - A boolean indicating whether an intrusion was detected (based on time and detections).

---

### `is_intrusion`

This method checks if an **intrusion** has occurred within the defined time range (`start_hour` to `end_hour`). If objects are detected during this period, it is considered an intrusion.

- **Parameter**: `nbr_detections` - The number of objects detected in the frame.
- **Returns**: `True` if an intrusion is detected, otherwise `False`.

---

### `plot_boxes`

This method draws **bounding boxes** around the detected objects in each frame. The boxes are colored based on the detected object's class (e.g., people).

- **Parameters**:
  - **`results`**: Detection results from YOLO.
  - **`img`**: The current frame on which to draw the boxes.
- **Returns**:
  - A list of detected objects with their coordinates.
  - The annotated image with bounding boxes.
  - The total number of detected objects.

---

## Usage Example

Here is an example of how to use the `Core_process` class, as shown in the **`test_object_detection.py`** file:

```python
from object_detection import Core_process

# Instantiate the Core_process class with an RTSP URL for an IP camera
detector = Core_process(capture="rtsp://192.168.1.100:554/stream1", confidence_threshold=0.5, person_only=True, start_hour=20)
```

This script captures the video stream from the specified **RTSP** URL, performs person detection with a confidence threshold of 0.5, and monitors intrusions starting from 8 PM.

---

## Author

This project was developed for real-time object and person detection using IP cameras (RTSP protocol) for surveillance purposes.

---
```

