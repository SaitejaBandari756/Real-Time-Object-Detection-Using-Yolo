
# Real-Time-Object-Detection-Using-Yolo

### End-to-end repository for training and testing a custom object detection model using the YOLO architecture. Demonstrates data preparation, hyperparameter tuning, and performance evaluation on custom datasets, starting with a COCO subset.
=======
**##🚀 Object Detection Using Yolov**

### 🎯 Project Overview
This repository provides an end-to-end pipeline for training and experimenting with state-of-the-art YOLO (You Only Look Once) models for object detection.The core purpose of this project is to establish a verified training environment, starting with a lightweight model and dataset, and then scaling efficiently to larger, custom applications.
**Key Features**
- YOLOv11 Architecture: Utilizes the lightweight YOLOv11-Nano (yolo11n) model for fast training and low resource consumption.
- Pipeline Validation: Uses the built-in COCO128 dataset (128 images) as a "sanity check" to ensure the entire training environment and configurations are correct.
- Custom Dataset Readiness: Structure is ready to integrate any custom dataset annotated in the standard YOLO format.
- Training and Metrics: Includes default configuration for training, validation, and outputting performance metrics (mAP, loss curves).
**🛠️ Prerequisites**
- Before running any training commands, ensure you have the required software installed.1. Python: Python 3.8+
2. PyTorch: The underlying deep learning framework.
3. Ultralytics Package: The official YOLO library.
**Installation**
It is highly recommended to use a virtual environment.
1. Install Ultralytics (YOLO framework):
> pip install ultralytics
### 🚀 Getting Started (Initial Run)
The primary goal of the initial run is to confirm your environment (including GPU/CUDA if available) is set up correctly. We use the small, built-in COCO128 dataset for this purpose.
1. Training CommandRun the following command from your terminal. The coco128.yaml and yolo11n.pt files will be downloaded automatically on the first execution.
> yolo detect train \
    data=coco128.yaml \
    model=yolo11n.pt \
    epochs=100 \
    imgsz=640

2. Output and Results
All training results are saved to a directory named `runs/detect/trainX/ (where X increments with each run).
- Weights: The final trained model files (`best.pt`, `last.pt`) are stored here.
- Logs: The `results.csv` file contains epoch-by-epoch metrics (loss, mAP).
- Plots: Plots showing loss curves, mAP progression, and confusion matrices.
### 📊 Next Steps: Scaling to a Custom Dataset
Once you have validated the pipeline using COCO128, follow these steps to use your own data:
1. Data Preparation (YOLO Format)Ensure your images and annotations are structured as follows
> :my_custom_data/
>>├── images/
>>│   ├── train/
>>│   └── val/
>>└── labels/
    >>├── train/
    >>└── val/
- Every image in `images/train` must have a corresponding `.txt` annotation file in `labels/train`.
2. Create a Custom YAML File
Create a file named `custom_data.yaml` in the repository root to define your dataset configuration:

> # custom_data.yaml
># Paths relative to the YOLO working directory
>path: /path/to/my_custom_data
>train: images/train
>val: images/val

># Number of classes
>nc: 2
># Map class IDs (0, 1) to names
>names: ['apple', 'banana']

3. Start TrainingUpdate the CLI command to reference your new YAML file:
>yolo detect train \
    >>data=custom_data.yaml \
    >>model=yolo11n.pt \
    >>epochs=50 \
    >>imgsz=640
You can now adjust parameters like `epochs` and the model size (e.g., switch to `yolo11s.pt` for higher accuracy) based on your custom task and hardware constraints.
