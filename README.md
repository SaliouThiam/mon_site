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
