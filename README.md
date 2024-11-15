# Textile Fabric Classification

This repository contains computer vision based Textile Fabric Detection and classification task, where fabric is classified in 6 different classes (cotton, denim, silk, leather, linen and nylon) 

## 1. Dataset Preparation and Labeling Process

### 1.1 Dataset Overview

The dataset used for this fabric detection and classification task was sourced from **Roboflow**, containing a total of **503 raw images**.

### 1.2 Labeling Process

The labeling of images was performed using **Roboflow's annotation tools**, which facilitate precise bounding box creation for each object of interest. The key steps included:

- **Image Upload:** The raw images were forked from another project to the Roboflow platform.
- **Annotation:** Each object within the images was previously labeled with bounding boxes. This included specifying the class labels for each object to ensure accurate detection during training.
- **Exporting Labels:** Once the labeling process was completed, the dataset was exported in YOLO format, which generates .txt files containing the coordinates of the bounding boxes corresponding to each image.

### 1.3 Data Augmentation

To enhance the robustness of the model and to prevent overfitting, data augmentation techniques were applied during preprocessing. The following augmentations were implemented:

- **Rotation:** Images were rotated at +15/-15 degree angles to simulate different orientations of objects.
- **Noise Addition:** Gaussian noise was introduced to the images, creating variations that mimic real-world conditions.

These augmentations increased the effective size of the training dataset and provided the model with diverse examples to learn from.

### Dataset link after Labeling and Augmentation: https://app.roboflow.com/fabric-fault-detection-paunj/fabric-qxgmo-init6/3

## 2. Model Architecture and Training Process

(Currently YOLOv11 model is implemented. Work with more models like CNN, ResNet in progress.)

### 2.1 YOLOv11

The model used for this task was based on the **YOLO (You Only Look Once) architecture** , specifically YOLOv11. YOLO is a real-time object detection system known for its speed and accuracy. The architecture includes:

- **Backbone:** A deep convolutional neural network that extracts features from the input images.
- **Neck:** Combines feature maps from different layers to enhance the detection performance across various scales.
- **Head:** YOLOv11 uses a multi-scale prediction head to detect objects at different sizes. The head outputs detection boxes for three different scales (low, medium, high) using the feature maps generated by the backbone and neck.

[source: https://medium.com/@nikhil-rao-20/yolov11-explained-next-level-object-detection-with-enhanced-speed-and-accuracy-2dbe2d376f71]

### 2.2 Training Process

The training process involved:

- **Model Initialization:** The YOLO model was initialized using pre-trained weights (yolo11n.pt) to leverage transfer learning.
- **Data Configuration:** A configuration file (data.yaml) was created to specify the paths to the training and validation datasets and to define the class names.
- **Training Execution:** The model was trained for **65 epochs** using RTX 3060 GPU. The training command utilized was:

```
model = YOLO("yolo11n.pt")
model.train(data="..\\fabric3\\data.yaml", epochs = 65 , device = 0)
```
- **Monitoring:** During training, metrics such as loss and mAP (mean Average Precision) were monitored to evaluate performance.

## 3. Performance Metrics and Improvements Made

### 3.1 Performance Metrics

To evaluate the performance of the trained YOLO model, the following metrics were calculated:

- **Mean Average Precision (mAP):** A higher mAP indicates better detection performance. In the test data the result is **92.1%**.
- **Precision and Recall:** In the test data total 146 instances are correctly detected out of 175 images. The **precision** value
    of 0.887 indicates that approximately **88.7%** of the predictions made by the model were correct, and **recall** of 0.79 shows that the model successfully detected **79%** of the actual instances.

### 3.2 Improvements Made

Throughout the training process, several improvements were implemented based on evaluation feedback:

- **Hyperparameter Tuning:** Adjustments were made to the number of epochs based on training observations.
- **Data Augmentation:** Additional augmentations were explored, including image rotation and adding noise to further enhance model robustness.

## 4. Challenges and Limitations Encountered

### 4.1 Challenges

- **Data Imbalance:** Some classes in the dataset had significantly fewer instances than others, which led to biased performance. This was addressed by employing data augmentation more heavily on underrepresented classes.

### 4.2 Limitations

- **Limited Dataset Size:** Although the dataset was augmented, the original size of 503
    images may still limit the model's ability to generalize to unseen data. Future work
    could involve collecting more data or using larger datasets.

## 5. Fabric Detection and Classification Demo

![Acr2_png rf b74f157fa82b42102a129b6537ca45b1](https://github.com/user-attachments/assets/cb9e69e9-8afc-4046-82e7-d3a5c4e99cd1)
![D46_png rf 7cf0fb6afcabbbe9884b958b9392e0aa](https://github.com/user-attachments/assets/b615bf1d-cefa-4968-a498-f9658e98fc51)

![l40_png rf caed1214e7a26430048613bd76ae7bd1](https://github.com/user-attachments/assets/25c75893-6426-479d-a062-5cc4dbadc6cf)
![N90_png rf 229f00e391ab3e5a8afe1c82d492b4c1](https://github.com/user-attachments/assets/e74f56e2-a7cf-4e98-a903-74916ef201bc)
