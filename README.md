# Autonomous Navigation - YOLO

## 🚀 Project Overview
This project focuses on **autonomous navigation** using **YOLO (You Only Look Once)** for object detection in a self-driving car simulation environment. The model is trained on the **Udacity self-driving car dataset** and processes **real-time vision-based inputs** to navigate safely while avoiding obstacles.

## 📌 Features
- **Dataset Processing**: Loads, processes, and organizes self-driving car datasets.
- **YOLOv8 Training**: Uses YOLOv8 for object detection and obstacle recognition.
- **Model Evaluation**: Analyzes performance using precision-recall metrics.
- **Dataset Augmentation**: Implements techniques like blurring, grayscale conversion, and contrast adjustments.
- **Autonomous Navigation**: Uses trained YOLOv8 model to guide navigation decisions.

## 📂 Dataset
The dataset is sourced from the [Udacity self-driving car dataset](https://www.udacity.com/self-driving-car) and contains annotated images of road environments with obstacles.

### 📁 Dataset Structure
```
/kaggle/input/udacity-self-driving-car-dataset/data/
 ├── export/
 │   ├── _annotations.csv   # Object annotations
 │   ├── images/            # Raw images
 └── README.roboflow.txt    # Dataset documentation
```

## 🛠️ Installation & Setup
Ensure you have **Python 3.8+** and install the required dependencies:

```sh
pip install ultralytics opencv-python pandas matplotlib numpy
```

Clone the repository and navigate to the project folder:
```sh
git clone https://github.com/PrageethM1702/Autonomous-Navigation.git
cd autonomous-nav-yolo
```

## 📌 Dataset Preprocessing
```python
import os
import pandas as pd
import shutil

dataset_path = "/kaggle/input/udacity-self-driving-car-dataset/data"
csv_source_path = f"{dataset_path}/export/_annotations.csv"
csv_download_path = "/kaggle/working/"
shutil.copy(csv_source_path, csv_download_path)
```

## 🏋️ Model Training
```python
from ultralytics import YOLO
model = YOLO("yolov8n.pt")
model.train(data="/kaggle/working/yolo_dataset/data.yaml", epochs=5, imgsz=512, batch=8, name="yolo_v8_model")
```

## 🎯 Model Evaluation
```python
metrics = model.val()
print("Model Accuracy:", metrics)
```

## 📈 Performance Metrics
| Epoch | Precision | Recall | mAP50 | mAP50-95 |
|--------|------------|--------|-------|------------|
| 1 | 0.342 | 0.400 | 0.307 | 0.168 |
| 2 | 0.516 | 0.461 | 0.448 | 0.247 |
| 3 | 0.551 | 0.529 | 0.512 | 0.292 |
| 4 | 0.603 | 0.573 | 0.586 | 0.340 |
| 5 | 0.658 | 0.607 | 0.641 | 0.380 |

## 🔧 Running the Model
```python
results = model.predict(source="/path/to/test/image.jpg", save=True)
```
