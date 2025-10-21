# T-Students FITDNU — A Classroom Student Behavior Detection Dataset
## 1) Introduction

**T-Students FITDNU** is a dataset for object/behavior detection in classroom environments, collected using **a single ceiling-mounted camera** (1080p@25fps) during real class sessions (morning/afternoon). The dataset emphasizes **small objects** (phones, computers) and **occlusions** due to crowded classrooms, making it valuable for evaluating **YOLO models** in real-world deployment scenarios.

- **9 classes:** `using_phone`, `using_computer`, `sleeping`, `turning_left`, `turning_right`, `raising_hand`, `writing`, `phone`, `computer`.
- **Scale:** **3,351 images**, **126,429** bounding boxes.
- **Goal:** Serve research and real-time demo purposes from a **single ceiling viewpoint**.

## 2) Class Distribution

<p align="center">
  <img src="Behavior and objects.png" alt="Example for each class" width="500"/>
  <br/>
</p>
<div align="center">

**Bounding box distribution by class:**

| No. | Class           | # of bbox |
|---:|------------------|----------:|
| 1 | Computer         | 20,100 |
| 2 | Phone            | 45,910 |
| 3 | Raising Hand     | 318    |
| 4 | Sleeping         | 4,826  |
| 5 | Turning Left     | 9,720  |
| 6 | Turning Right    | 9,222  |
| 7 | Using Computer   | 8,412  |
| 8 | Using Phone      | 23,709 |
| 9 | Writing          | 4,212  |

</div>


> The dataset is **intentionally imbalanced** to reflect natural frequency — useful for Focal Loss, re-weighting, oversampling, copy-paste, etc.  
**Roboflow Universe:** open the dataset page (**[Link](https://universe.roboflow.com/tstudentsfitdnu/t-students-fitdnu/dataset/1)**), choose a **Version** and **Export Format** (YOLOv5/YOLOv8/COCO JSON/VOC…), and download via UI or API.

## 3) Model Training Results
<div align="center">
| Activity        | Model        | Precision | Recall | mAP@0.5 | mAP@[0.5:0.95] |
|-----------------|--------------|----------:|------:|--------:|---------------:|
| **Phone**           | Faster R-CNN | 31.4 | 38.9 | 7.8  | 31.4 |
|                   | YOLOv7       | 86.8 | 77.9 | 83.2 | 42.1 |
|                   | YOLOv8l      | **89.6** | **78.9** | **87.9** | **43.7** |
|                   | YOLOv12s     | 86.2 | 62.0 | 73.3 | 43.7 |
| **Using Phone**    | YOLOv7       | 92.1 | 94.9 | 96.9 | 67.1 |
|                   | YOLOv8l      | **95.5** | **95.8** | **97.7** | **81.0** |
|                   | YOLOv12s     | 87.8 | 92.8 | 93.6 | 67.1 |
| **Computer**       | Faster R-CNN | 58.6 | 66.9 | 15.7 | 58.6 |
|                   | YOLOv7       | 94.1 | 96.6 | 97.0 | 66.1 |
|                   | YOLOv8l      | **96.4** | **98.2** | **98.6** | **79.1** |
|                   | YOLOv12s     | 93.6 | 96.5 | 96.5 | 70.5 |
| **Turning Left**   | Faster R-CNN | 43.4 | 54.3 | 27.6 | 43.4 |
|                   | YOLOv7       | 91.6 | 91.4 | 96.2 | 61.8 |
|                   | YOLOv8l      | **94.8** | **95.7** | **97.5** | **80.7** |
|                   | YOLOv12s     | 84.3 | 85.3 | 88.9 | 58.7 |
| **Turning Right**  | Faster R-CNN | 40.3 | 51.3 | 28.4 | 40.3 |
|                   | YOLOv7       | 88.2 | 90.7 | 94.4 | 59.9 |
|                   | YOLOv8l      | **94.1** | **93.4** | **96.4** | **78.8** |
|                   | YOLOv12s     | 83.6 | 83.7 | 87.6 | 58.6 |
| **Using Computer** | Faster R-CNN | 54.4 | 64.2 | 23.3 | 54.4 |
|                   | YOLOv7       | 87.0 | 96.3 | 96.3 | 69.7 |
|                   | YOLOv8l      | **95.2** | **94.9** | **97.6** | **82.6** |
|                   | YOLOv12s     | 85.2 | 90.2 | 92.0 | 69.1 |
| **Sleeping**       | Faster R-CNN | 55.9 | 63.4 | 51.0 | 55.9 |
|                   | YOLOv7       | 92.4 | 96.4 | 96.1 | 65.8 |
|                   | YOLOv8l      | **96.5** | **98.8** | **98.9** | **82.6** |
|                   | YOLOv12s     | 91.7 | 92.4 | 96.4 | 69.7 |
| **Writing**        | Faster R-CNN | 48.2 | 57.4 | 40.7 | 48.2 |
|                   | YOLOv7       | 89.7 | 92.7 | 95.5 | 63.3 |
|                   | YOLOv8l      | **93.8** | **93.1** | **95.6** | **78.2** |
|                   | YOLOv12s     | 83.4 | 86.9 | 88.0 | 48.4 |
| **Raising Hand**   | Faster R-CNN | 25.5 | 33.9 | 39.9 | 25.5 |
|                   | YOLOv7       | **90.9** | **83.1** | **87.6** | **70.3** |
|                   | YOLOv8l      | 84.4 | 96.2 | 95.7 | 70.3 |
|                   | YOLOv12s     | 61.2 | 34.6 | 52.9 | 39.0 |
</div>
### General Observations
- **YOLOv8l** achieves the **highest overall mAP@[0.5:0.95]**, especially excelling in subtle behaviors or small objects (*sleeping*, *turning_left/right*, *using_computer*).
- **YOLOv7** performs well on frequent classes (*using_phone*), but performance drops on rare ones (*raising_hand*).
- **YOLOv12s** is a **lightweight and fast** option, ideal for real-time deployment.
- **Faster R-CNN** struggles with **occlusion and crowded classroom scenes**, leading to low mAP in *phone* and *raising_hand* classes.

## 4) Contact

- Dataset/Paper: **tu05062005@gmail.com**
- For technical issues: open an **Issue** in this repository.
